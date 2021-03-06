There is ample detailed information out there on installing wordpress. However, I wanted to just provide a small supplement about setting up two distinct wordpress blogs within a single apache2 web site. The system I am using is Ubuntu Linux 8.10, but other than the package installation, the configuration steps should be the same on other linux distributions.

As a first step, read through the [Wordpress Installation Instructions](http://codex.wordpress.org/Getting_Started_with_WordPress#Installation). You will find them to be thorough and clear. The starting point for my setup is that I already had a web site up and running under apache2\. I just wanted to add the Wordpress (and underlying MySQL database) setup and have two separate blogs with separate themes and content.

So here's my starting setup:

*   Ubuntu 8.10 on an amd64 system
*   apache2 already installed and working
*   static content for the web site deployed in `/var/www/example.com`
*   MySQL and Wordpress are not yet installed

#### Install wordpress and mysql

First let's install wordpress and mysql. I'll do this on the command line using the `apt-get` program, but you can [use one of the graphical options as well](https://help.ubuntu.com/8.10/add-applications/C/advanced.html)

<pre>sudo apt-get install wordpress virtual-mysql-server</pre>

You should see a bunch of packages that will get installed and press `y` to proceed. The MySQL install will prompt you to create a new mysql root account password, so go ahead and do that.

#### Set up the wordpress databases

OK, so let's say we are going to call our blogs blog1 and blog2\. We need to create mysql databases for them. Note that you may see tutorials telling you you can store the data for two separate blogs in one database. While true, two databases is a much cleaner way to go. End users shouldn't be going around making up database table names. So, we are going to use the mysql command line tools to do this. Again, the wordpress docs here are fine and describe graphical alternatives as well. Let's connect to mysql (use the password you created above) as root and create the databases. We'll call them blog1 and blog2 and we'll also set up user accounts inside mysql that wordpress will use to access the databases. Again for simplicity, we'll also call the user accounts blog1 and blog2\. Replace "MakeUpPassword" with your own chosen password.

<div class="code">

<pre>mysql -u root -p
create database blog1;
GRANT ALL PRIVILEGES ON blog1.* TO "blog1"@"localhost" IDENTIFIED BY "MakeUpPassword";
flush privileges;
create database blog2;
GRANT ALL PRIVILEGES ON blog2.* TO "blog2"@"localhost" IDENTIFIED BY "MakeUpPassword";
flush privileges;
quit;
</pre>

</div>

#### Install wordpress files and configure DB access

OK, when we installed wordpress above, Ubuntu put a copy of the wordpress PHP files into `/usr/share/wordpress`, so now we're going to make 2 copies, one for each blog, underneath our web site's document root. Note that since these are two blogs in the same web site, we don't want either blog to be the top level home page of the site, so each gets its own separate subdirectory.

<div class="code">

<pre>sudo mkdir -p /var/www/example.com/blog1 /var/www/example.com/blog2
sudo cp -r /usr/share/wordpress/* /var/www/example.com/blog1
sudo cp -r /usr/share/wordpress/* /var/www/example.com/blog2
sudo chown -R www-data:www-data /var/www/example.com/blog*
</pre>

</div>

Now I should note that Debian/Ubuntu has a customized wordpress configuration. Often, these are well crafted by the experts and will save you a lot of time and hassle if you follow the patterns they suggest. In this case, I don't think their setup exactly matches my goal of two different blogs under one web site, so I am bypassing their pattern and doing my own simple alternative. So what happens is that by default the file `/usr/share/wordpress/wp-config.php is a symbolic link to /etc/wordpress/wp-config.php`, and when we copied these files, that symlink was copied too, which means if we aren't careful both of our blogs will point at the same database, making them one blog instead of two! So we do the following:

<div class="code">

<pre>sudo rm /var/www/example.com/blog*/wp-config.php
sudo cp /usr/share/wordpress/wp-config-sample.php /var/www/example.com/blog1/wp-config.php
sudo cp /usr/share/wordpress/wp-config-sample.php /var/www/example.com/blog2/wp-config.php
sudo chown -R www-data:www-data /var/www/example.com/blog*
</pre>

</div>

OK, now each blog has it's own separate copy of wp-config.php. Go ahead and edit those files to point blog1 at the blog1 database and blog2 at the blog2 database using vi or your text editor of choice. When done, they should look as follows:

<pre>/var/www/example.com/blog1/wp-config.php</pre>

<div class="code">

<pre><?php
// ** MySQL settings ** //
define('DB_NAME', 'blog1');    // The name of the database
define('DB_USER', 'blog1');     // Your MySQL username
define('DB_PASSWORD', 'yourpasswordhere'); // ...and password
define('DB_HOST', 'localhost');    // 99% chance you won't need to change this value
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');

// Change SECRET_KEY to a unique phrase.  You won't have to remember it later,
// so make it long and complicated.  You can visit http://api.wordpress.org/secret-key/1.0/
// to get a secret key generated for you, or just make something up.
// Change this to a unique phrase.
define('SECRET_KEY', 'put your unique phrase here -- yes you change this now');

// You can have multiple installations in one database if you give each a unique prefix
$table_prefix  = 'wp_';   // Only numbers, letters, and underscores please!

// Change this to localize WordPress.  A corresponding MO file for the
// chosen language must be installed to wp-content/languages.
// For example, install de.mo to wp-content/languages and set WPLANG to 'de'
// to enable German language support.
define ('WPLANG', '');

/* That's all, stop editing! Happy blogging. */

define('ABSPATH', dirname(__FILE__).'/');
require_once(ABSPATH.'wp-settings.php');
?>
</pre>

</div>

<pre>/var/www/example.com/blog2/wp-config.php</pre>

<div class="code">

<pre><?php
// ** MySQL settings ** //
define('DB_NAME', 'blog2');    // The name of the database
define('DB_USER', 'blog2');     // Your MySQL username
define('DB_PASSWORD', 'yourpasswordhere'); // ...and password
define('DB_HOST', 'localhost');    // 99% chance you won't need to change this value
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');

// Change SECRET_KEY to a unique phrase.  You won't have to remember it later,
// so make it long and complicated.  You can visit http://api.wordpress.org/secret-key/1.0/
// to get a secret key generated for you, or just make something up.
// Change this to a unique phrase.
define('SECRET_KEY', 'put your unique phrase here -- yes you change this now');

// You can have multiple installations in one database if you give each a unique prefix
$table_prefix  = 'wp_';   // Only numbers, letters, and underscores please!

// Change this to localize WordPress.  A corresponding MO file for the
// chosen language must be installed to wp-content/languages.
// For example, install de.mo to wp-content/languages and set WPLANG to 'de'
// to enable German language support.
define ('WPLANG', '');

/* That's all, stop editing! Happy blogging. */

define('ABSPATH', dirname(__FILE__).'/');
require_once(ABSPATH.'wp-settings.php');
?>
</pre>

</div>

#### Permalinks

OK, now let's make sure we have mod_rewrite enabled for wordpress permalinks, then we restart apache2 to get our new software and config to take effect. We'll also make sure we have a writeable .htaccess file so wordpress can set it up for us.

<div class="code">

<pre>sudo a2enmod rewrite
sudo apache2ctl restart
sudo touch /var/www/example.com/blog1/.htaccess
sudo touch /var/www/example.com/blog2/.htaccess
sudo chown www-data:www-data /var/www/example.com/blog*/.htaccess
sudo chmod 644 /var/www/example.com/blog*/.htaccess
</pre>

</div>

Almost done, we can now point a web browser to [http://localhost/blog1/wp-admin/install.php](http://localhost/blog1/wp-admin/install.php) and fill out that form and launch the wordpress self-install. Repeat the process for blog2 at [http://localhost/blog2/wp-admin/install.php](http://localhost/blog2/wp-admin/install.php). Now, this is going to set up the blog in the database and create the admin user with a default password. If your computer has a mail transport agent running, you should get the email with the default password. If not, you won't, which is what happened to me, so we can just set the admin password to one of our choosing. First, we need to know the MD5 checksum of our chosen password. You can use [this online form](http://epleweb.com/md5/) to get the MD5 of your password, but sending your password to some random web site in clear text is too insecure for me. Therefore, if you have python, you can use this little python one-liner to do it. This will securely prompt you for your password and print out the corresponding MD5\. Nothing is sent over the network. You will end up with a 32-character hex string. Use this instead of the For details from wordpress, read [resetting your password](http://codex.wordpress.org/Resetting_Your_Password) in the wordpress online docs. The cheat sheet is below.

<pre>python -c "import getpass,md5;m=md5.new();m.update(getpass.getpass());print m.hexdigest()"</pre>

OK, so let's set this password into mysql so we can start managing our blog

<div class="code">

<pre>mysql -u root -p
use blog1;
update wp_users set user_pass="useyour32charhexstringmd5here" where user_nicename="admin";
use blog2;
update wp_users set user_pass="useyour32charhexstringmd5here" where user_nicename="admin";
quit;
</pre>

</div>

OK, you are good to go to [http://localhost/blog1](http://localhost/blog1), log in as admin, and start managing your blog. You can go in and set up custom pretty permalinks in the admin section and when you save, wordpress should be able to write the rewrite settings to the .htaccess file we set up for you. Good luck and happy blogging!
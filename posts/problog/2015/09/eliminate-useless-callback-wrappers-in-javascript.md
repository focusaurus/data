Just a quick tip from some code I encountered today. Instead of this:


    function outerFunc (callbacj) {
      doSomething(42, function (err) {
        callback(err)
      })
    }

Eliminate the useless callback wrapper function:

    function outerFunc (callbacj) {
      doSomething(42, callback)
    }

It's more concise and more efficient and entirely equivalent.

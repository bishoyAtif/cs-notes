# ES6 : ECMAScript 6

 npm install --devDependencies vs --dependencies
devDependencies : for parts of the app that you might need as a developer to build/test/compile/serve the app. Things like your test suite or your gulp/other task runners.
dependency for anything that the client needs to run the compiled app. In your case, both Angular and Angular datepicker are dependencies. In other words, They are the dependencies to be run in the runtime.


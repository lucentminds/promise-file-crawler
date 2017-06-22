# promise-file-crawler
Promise-based file system crawler. This is the proposed useage.

## Installation
~~~shell
npm install git+https://github.com/lucentminds/promise-file-crawler.git
~~~

## Useage:
~~~js
var crawler = require( 'promise-file-crawler' );

crawler.scan( {
   // Top level dir to start crawling.
   root: '/',

   // Files per second. 0 for full speed.
   fps: 0,

   // Only care about txt files.
   filter: [
      /\.txt$/
   ],
   
   // Determines how many workers/threads are active at one time.
   workers: 2

}, function( oResult, next ){

   // Here is where you process one located file.
   console.log( oResult );

   doSomethingAsync( oResult.filename, function( err, result ){
      if( err ) {
         return console.log( 'Error:', err );
      }

      console.log( 'Success!' );

      // Release this worker to continue crawling.
      next();
   });

})
.then(function(){
   console.log( 'Finished!' );
});
~~~
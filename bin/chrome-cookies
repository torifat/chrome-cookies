#!/usr/bin/env node

var fs = require( 'fs' ),
    path = '';

switch( process.platform ) {
  case 'darwin':
    path = process.env.HOME + '/Library/Application Support/Google/Chrome/Default/Cookies';
    break;
  case 'linux':
    path = process.env.HOME + '/.config/google-chrome/Default';
    break;
  default:
    console.error( 'Currently your OS is not supported!' );
    process.exit( 1 );
}

var url = process.argv[process.argv.length - 1],
    matches = url.match( /:\/\/([\w\.-]+)/ );

if( !matches ) {
  console.error( 'Invalid url! Please provide a valid url' );
  process.exit( 1 );
}

if( !fs.existsSync( path ) ) {
  console.error( 'I don\'t think you have Google Chrome installed!' );
  process.exit( 1 );
}

var sqlite3 = require( 'sqlite3' ).verbose(),
    db = new sqlite3.Database(path),
    tld = require( 'tldjs' ),
    host = '.' + tld.getDomain( matches[1] );

db.serialize(function() {
  db.each( "SELECT host_key, path, secure, expires_utc, name, value FROM cookies where host_key like '%" + host + "%'", function( err, cookie ) {
    if ( err ) {
      throw err;
    }
    var out = cookie.host_key + '\t' +
    ( cookie.host_key.indexOf( host ) === 0 ? 'TRUE' : 'FALSE' ) + '\t' +
    cookie.path + '\t' +
    ( !!cookie.secure ? 'TRUE' : 'FALSE') + '\t' +
    ( !!cookie.expires_utc ? cookie.expires_utc : '0') + '\t' +
    cookie.name + '\t' +
    cookie.value + '\n';
    console.log( out );
  });
});

db.close();
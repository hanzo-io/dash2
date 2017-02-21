require 'shortcake'

use 'cake-test'
use 'cake-version'
use 'cake-publish',
  deploy:
    remote:  'origin'
    refspec: 'master:master'
  npm: false

task 'build:pre', '', ->
  exec '''
       mkdir -p public/css
       mkdir -p public/js
       '''

task 'build', 'build project', ['build:pre'], ->
  exec 'bebop compile'

task 'build:min', 'build js for production', ['build'], ->
  exec 'uglifyjs public/js/app.js --compress --mangle --lint=false > public/js/app.js'

task 'watch', 'watch for changes and recompile project', ['build:pre'], ->
  exec 'bebop'

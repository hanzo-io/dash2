require 'shortcake'

use 'cake-bundle'
use 'cake-linked'
use 'cake-outdated'
use 'cake-test'
use 'cake-version'

use 'cake-publish',
  deploy:
    remote:  'origin'
    refspec: 'master:master'
  npm: false

task 'build', 'build project', ['build:static', 'build:js']

task 'build:js', 'build js', ->
  return if (running 'build')

  bundle.write
    entry:    'src/js/app.coffee'
    dest:     'public/js/app.js'
    cache:    false
    format:   'web'
    commonjs: true
    external: false
    compilers:
      coffee:
        version: 1
  .catch (err) ->
    console.error err

task 'build:static', 'build static assets', ->
  exec '''
    mkdir -p public/css
    mkdir -p public/js
    bebop compile'
  '''

task 'watch', 'watch for changes and rebuild project', ['watch:js', 'watch:static']

task 'watch:js', 'watch js for changes and rebuild', ->
 build = (filename) ->
    return if (running 'build')
    console.log filename, 'modified'
    invoke 'build:js'

  watch 'src/*',          build
  watch 'node_modules/*', build

task 'watch:static', 'watch static files and rebuild', ['build:static'], ->
  exec 'bebop'

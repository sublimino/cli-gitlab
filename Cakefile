{spawn, exec} = require 'child_process'

call = (command, args = [], fn = null) ->
  exec "#{command} #{args.join(' ')}", (err, stdout, stderr) ->
    if err?
      console.error "Error :"
      return console.dir   err
    fn err if fn

system = (command, args) ->
  spawn command, args, stdio: "inherit"

build = (fn = null) ->
  call 'coffee',     ['-bco', 'bin', 'bin']

watch = (fn = null) ->
  system 'coffee',     ['-wbco', 'bin', 'bin']

task 'watch', 'continually build the JavaScript code', ->
  watch ->
    console.log "Done !"

task 'build', 'build the JavaScript code', ->
  build ->
    console.log "Done !"

task 'doc', 'rebuild the Docco documentation', ->
    exec([
        'docco src/*.coffee'
    ].join(' && '), (err) ->
        throw err if err
    )

# A sample Guardfile
# More info at https://github.com/guard/guard#readme

# Add files and commands to this file, like the example:
#   watch(%r{file/path}) { `command(s)` }
#

require 'blinky_tape_test_status/guard'

notification :file, :path => '.guard_result'

guard :shell do
  watch('.guard_result') { @blinky_tape.set_status! }

  callback(:start_begin) {
    @blinky_tape = BlinkyTapeTestStatus::Guard.new :filename => File.expand_path('.guard_result')
    @blinky_tape.rainbow!
  }
  callback(:reload_begin) { @blinky_tape.rainbow! }
  callback(:stop_begin) { @blinky_tape.shutdown! }
end

guard :rspec do
  watch(%r{^spec/.+_spec\.rb$})
  watch('spec/spec_helper.rb')  { "spec" }

  callback(:run_all_begin) { @blinky_tape.pulse! }
  callback(:run_all_end) { @blinky_tape.set_status! }
  callback(:run_on_modifications_begin) { @blinky_tape.flash! }
  callback(:run_on_modifications_end) { @blinky_tape.set_status! }
end


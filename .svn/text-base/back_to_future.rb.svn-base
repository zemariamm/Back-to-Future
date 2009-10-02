require 'rubygems'
require 'activesupport'

=begin
# Simple Usage
require 'rubygems'
require 'activesupport'

want_to_go =  Time.now - 40.years - 18.days

puts "Current time: " + Time.now.to_s

BackToFuture::back_to_future(want_to_go) do 
puts "In the future " + Time.now.to_s
end

puts "back :" + Time.now.to_s
=end


module BackToFuture
  def back_to_future(moment)
    def Time.metaclass
        class << self; self; end
      end
    class << Time
      alias :old_now :now
    end

    tmeta = Time.metaclass

    tmeta.class_eval <<-END
  def now
    val = "#{moment}"
    Time.parse(val,now=val)
  end
  END

  yield
  class << Time
    alias :now old_now
  end
 end
module_function :back_to_future
end

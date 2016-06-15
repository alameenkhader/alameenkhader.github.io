---
layout: post
title:  "Exception Notification in Background Jobs"
date:   2016-06-15 02:44:26 +0530
categories: Rails ActiveJob Exception Notification
---
How to configure the [exception_notification] [exception-notification] gem for the background jobs.

{% highlight ruby %}
# app/jobs/application_job.rb
# ApplicationJob
class ApplicationJob < ActiveJob::Base
  queue_as :default

  rescue_from StandardError do |exception|
    logger.error format(
      'Exception Occured (%s) in processing %s', exception.message,
      self.class)
    ExceptionNotifier.notify_exception(exception)
  end

  # handles deleted records
  rescue_from ActiveJob::DeserializationError do
    logger.error format('DeserializationError in %s!', self.class)
  end
end
{% endhighlight %}

{% highlight ruby %}
# OrderAvailableJob
class OrderAvailableJob < ApplicationJob
  # Comparing pick up time to prevent the job from making the job available
  #   incase the pick up time was updated
  def perform(order, order_pick_up_time_secs = nil)
    return if order.admin_canceled?

    return unless order_pick_up_time_secs.eql?(order.pick_up_time.try(:to_i))

    order.make_available(true)
  end
end
{% endhighlight %}

#### References
* [exception_notification] [exception-notification]
* [Rails ActiveJob] [rails-active-job]

[exception-notification]: https://github.com/smartinez87/exception_notification
[rails-active-job]: https://github.com/rails/rails/tree/master/activejob

---
layout: post
title:  "Rspec Built in Matchers"
date:   2016-07-14 02:44:26 +0530
categories: Rails Rspec Matchers
---
### Arrays
{% highlight ruby %}
  describe Order do
    describe '.delivered' do
      let!(:delivered_orders) { create_list(:order, 3, delivered: true) }
      let!(:other_orders) { create_list(:order, 3) }

      it { expect(described_class.delivered).to match_array(delivered_orders) }
    end
  end
{% endhighlight %}

#### References
* [exception_notification] [exception-notification]
* [Rails ActiveJob] [rails-active-job]

[exception-notification]: https://github.com/smartinez87/exception_notification
[rails-active-job]: https://github.com/rails/rails/tree/master/activejob

---
layout: post
title:  "Rspec Cheat Sheet"
date:   2016-07-14 02:44:26 +0530
categories: Rails Rspec 
---
### Arrays
```
  describe Order do
    describe '.delivered' do
      let!(:delivered_orders) { create_list(:order, 3, delivered: true) }
      let!(:other_orders) { create_list(:order, 3) }

      it { expect(described_class.delivered).to match_array(delivered_orders) }
    end
  end
```

## Stubbing
```
allow(AssignDriverJob).to receive(:perform_later).and_return(true)
```

## Expect changes
```
# expect changes
expect { Counter.increment }.to change { Counter.count }.from(0).to(1)
# expect no changes
expect { Counter.increment }.to_not change { Counter.count}.from(0).to(1)
expect { Counter.increment }.to_not change { Counter.count}
```

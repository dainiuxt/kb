# Ruby/Rails

``` ruby
today = Date.today
#=> Mon, 03 Oct 2022
today.end_of_week
#=> Sun, 09 Oct 2022
today.beginning_of_month
#=> Sat, 01 Oct 2022
today.end_of_quarter
#=> Sat, 31 Dec 2022
today.beginning_of_year
#=> Sat, 01 Jan 2022
today.all_day
#=> Mon, 03 Oct 2022 00:00:00.000000000 UTC +00:00..
#=> Mon, 03 Oct 2022 23:59:59.999999999 UTC +00:00
today.all_week
#=> Mon, 03 Oct 2022..Sun, 09 Oct 2022
today.all_month
#=> Sat, 01 Oct 2022..Mon, 31 Oct 2022
today.all_year
#=> Sat, 01 Jan 2022..Sat, 31 Dec 2022
today.on_weekday?
#=> true
today.next_occurring(:thursday)
#=> Thurs, 06 Oct 2022

# …and DateTime:

right_now = Time.zone.now
#=> Mon, 03 Oct 2022 08:30:23.666835000 UTC +00:00
right_now.beginning_of_day
#=> Mon, 03 Oct 2022 00:00:00.000000000 UTC +00:00
right_now.end_of_week
#=> Sun, 09 Oct 2022 23:59:59.999999999 UTC +00:00
right_now.beginning_of_month
#=> Sat, 01 Oct 2022 00:00:00.000000000 UTC +00:00
right_now.end_of_quarter
#=> Sat, 31 Dec 2022 23:59:59.999999999 UTC +00:00
right_now.beginning_of_year
#=> Sat, 01 Jan 2022 00:00:00.000000000 UTC +00:00
right_now.all_day
#=> Mon, 03 Oct 2022 00:00:00.000000000 UTC +00:00..
#=> Mon, 03 Oct 2022 23:59:59.999999999 UTC +00:00
today.all_week
#=> Mon, 03 Oct 2022 00:00:00.000000000 UTC +00:00..
#=> Sun, 09 Oct 2022 23:59:59.999999999 UTC +00:00
today.all_month
#=> Sat, 01 Oct 2022 00:00:00.000000000 UTC +00:00..
#=> Mon, 31 Oct 2022 23:59:59.999999999 UTC +00:00
right_now.all_year
#=> Sat, 01 Jan 2022 00:00:00.000000000 UTC +00:00..
#=> Sat, 31 Dec 2022 23:59:59.999999999 UTC +00:00
right_now.on_weekday?
#=> true
right_now.next_occurring(:thursday)
#=> Thurs, 06 Oct 2022 08:30:23.666835000 UTC +00:00
```


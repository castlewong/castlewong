## Build a scrollable view

![](https://miro.medium.com/v2/resize:fit:1400/0*Z5-W1dgVsQhothLW)

Photo by [Jazmin Quaynor](https://unsplash.com/@jazminantoinette?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

First time trying out SwiftUI and figured I would make some sort of task management app. I wanted to make a header similar to the Calendar app on iOS devices — most importantly to achieve the top scrollable week view.

The preview below is the main goal for this post. The header part showing days on a week is what we want to achieve using only SwiftUI. Something that can be mentioned first is that this can be easily achieved using a library called [CalendarKit](https://github.com/richardtop/CalendarKit) which will look exactly the same as the native Calendar app but that is not our goal here.

![](https://miro.medium.com/v2/resize:fit:1170/1*ravYS-n7zGIaN_1ueJCx_A.jpeg)

The top part and scroll effect that we want to achieve

## **Creating the Model**

To start off we have to create a new struct `WeekValue` that holds the date of a week and an id as an identifier.

We need to do this as an array of `Dates` can’t be iterated (迭代) when trying to create views using `ForEach()` as they don’t conform to the `identifiable` protocol which means we need to be able to identify them.

WeekValue

## **Creating an ObservableObject to Manage Date Data**

After that’s done we can move ahead to the next part which is to create an `ObservableObject` that will manage all the data which are arrays of dates in this case that go into the view we want to build.

To achieve this we create some variables that will help manage the flow and to generate the weeks when swiped.

The method I came up with for this was to have 3 views that loop and just generate the dates as they are swiped. I got this idea from seeing a [post](https://stackoverflow.com/questions/72343827/carousel-view-swiftui) that implemented a looping carousel view and thought this might work.

WeekStore

Most of the functions and methods I used above aren’t as optimized as I wanted them to be but for the moment it works so I will be updating it when new ideas pop up.

The initial functions, in this case, are used to generate the starting weeks and append them to the array allWeeks that we have.

And so how this works is that we have three arrays of the `WeekValue` struct we created earlier that holds the dates of the week we need that being the current, previous, and next week and with this, we can update the array of dates in each of the when a swipe is done.

## **Creating the CustomView**

CustomHeaderView

Lastly, we have the main view for the `CustomWeekView` that holds two State variables `snappedItem`, and `draggingItem` which are used to position and move the view as we swipe them, to read more on this I use the [post](https://stackoverflow.com/questions/72343827/carousel-view-swiftui) I mentioned before as main reference.

This view works by using a loop of the three arrays of `allWeeks` that we generated on the `WeekStore` struct to then have another loop that generates Text based on the date it has which is exactly seven times the number of days in a week.

To generate the other weeks all we have to do is swipe or `DragGesture` in this case and on the `.onEnded` property of the gesture itself we call a function from `WeekStore` called `update()` which manages what to insert to the array of dates.

![](https://miro.medium.com/v2/resize:fit:1200/1*q2vz6C8mQnPODS8pyTqY-w.gif)

Demo

The animation itself doesn’t look the best but with some tweaking, it can definitely be fixed or even use another method to display the views of the dates.

Another method I tried was to use a `TabView` that updates when the index changes but still the animation doubles as when the index is updated the view refreshes. I also tried to create the view beforehand by creating a large enough Int value so it doesn’t refresh itself but that is definitely not optimized.

That is all from this post, again I mainly used this for a personal app I created to also help me understand SwiftUI. Most of the functions can still be refactored to create a cleaner code and most of the methods I used can be optimized but for now, I will keep it this way. I also hope this helps as I didn’t find a lot of resources regarding this topic.

## **References**

[https://stackoverflow.com/questions/72343827/carousel-view-swiftui](https://stackoverflow.com/questions/72343827/carousel-view-swiftui)
It's not every day a world-renowned football club tells you you can go ahead and launch your web app, but last week my latest web project was green-lit by Manchester United.

---
My boss and the CEO of [Gofamer](https://gofamer.com), Jere, is a huge Man U fan and he runs the only Manchester United museum in Finland, called the [Helsinki Red Room](https://helsinkiredroom.com). 

Through a sequence of events improbable and complex enough to warrant their own book, Jere is taking some items from his collection of memorabilia over to New York, San Diego and Las Vegas to show to fans over there at the end of this month. This is with the support and blessing of the club itself.

To get to my involvement: Jere wanted a web app to show off the items in his collection and to give extra information, ticket booking, competitions etc.

![Red Room on tour app](/assets/tour.png)

The app is intended to be simple enough - essentially a LinkTree-style single pager with buttons to point externally.

I forked the repo of someone's recent homegrown LinkTree to act as the scaffolding - this was set up with React and Tailwind (great for prototyping quickly) and had the rough layout I needed. I was quickly about to theme the interface to reflect the Helsinki Red Room's colours and styles, and find a Google Font that echoed that of the logo (as a side note, the font I went with '[Nobile](https://fonts.google.com/specimen/Nobile/about)' was inspired by the work of William Morris, whose childhood house I live around the corner from).

When I was then informed we wanted ticketing, I was able to quickly embed the 'buy' widget from [Ticketlab](https://ticketlab.co.uk) for the venues concerned (we're also being supported by Marriott Hotels who will house the collection in the different cities throughout this escapade).

This event is Ticketlab's first foray into the United States, which is hopefully somewhere we can continue to expand over the coming years.

The project was live within a week (around other projects and commitments) and will be updated with the memorabilia collection in the next couple of days.

You can [view the code](https://github.com/Rillus/helsinki-red-room) or view the [live version](https://tour.helsinkiredroom.com/) in it's current incarnation.
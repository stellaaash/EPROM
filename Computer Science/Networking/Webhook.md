A webhook is **a [[HyperText Transfer Protocol]] callback**, a way for a website to tell a program something is ready.
# Use Case
Instead of *polling*, as in repeatedly checking "has anything changed?", webhooks allow applications to **get a notification when things are ready**, via a `POST` request.
Here's the usual workflow:
- You register a [[Uniform Resource Locator]] with a service: "When X happens, POST to this endpoint"
- The event occurs on their system
- They immediately send an HTTP request to your URL with event data
- Your server receives it and does whatever it needs to do
This makes it **more efficient than polling**, since the party that actually knows the information (whether that thing you're waiting on is ready) sends the notification.
It's like telling your friend to "tell you" when you can call them, rather than trying to call them every minute to check if they're finally ready to talk.
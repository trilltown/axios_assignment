# Five (or more, or less) Card Draw

Today, we're going to be working with the [Deck of Cards API](https://deckofcardsapi.com/). It's a foundational skill for us, as programmers, to learn how any particular API works from some time testing it out, so take 15 minutes or so to look at the API documentation and play around with it in Postman.

Today, we're going to create an app that does three things:

- Creates and shuffles a new deck when the page loads.
- Includes a button to draw some cards from that deck.
- Displays those cards to the user.
- When the user clicks the button again, draws another set of cards from that same deck.

Let's break this down into smaller problems, shall we?

## Creating and Saving A Deck

When your page first loads, you should generate a new shuffled deck from the Deck of Cards API. The route to hit to accomplish this, according to the Deck of Cards docs, is this: `https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1`. Use Axios.

The response from that route should give you several parameters, but the only one that we really should care about is `deck_id`. With this `deck_id`, the Deck of Cards API is going to give us five cards from _that specific deck_ when we draw them. If we draw another five cards, it'll draw the next five unique cards from that deck. The API, in other words, is keeping track of this information for us.

However, we can't query this API multiple times for that deck if we don't save it. Go ahead and save the `deck_id` in a variable. Remember not to do this manually - **whenever the user refreshes the page, we should query the API for a new deck and save our new `deck_id`.**

## Drawing Cards

The next thing we'd like to do is to draw cards from our deck. Using our `deck_id`, the Deck of Cards API lets us draw one or more cards from the deck that we just created. The route for drawing five cards should look something like this: `https://deckofcardsapi.com/api/deck/~deck_id~/draw/?count=5`, where `~deck_id~` is the `deck_id` item we saved. Replace your `deck_id` and use Axios to query this route and log the response you receive to the console.

What is available to us here in the response? Well, again, we have only one key in this response that we really care about - `cards`, which contains an array of `Card` objects. Each of these `Card` objects have a set of parameters, all of which could prove useful to us, depending on what we want to do with them: There's an `image` URL, which links to a picture of the card. There's a `value` and `suit` parameter, and then there's a `code` parameter with shorthand should we need it.

Create a `button` tag in your HTML. When you click on this `button`, you should fire your Axios request to draw five cards. Save them to a variable in your project. When you click the button again, you should draw five different cards and save them to the same variable, overwriting your previous cards. Log this variable to the console so you know what you're doing.

## Rendering Cards to the DOM

When we click, we should see the images of five cards, in a row, underneath our button. This should be familiar to you from our Dog API image rendering. In your button event listener, inside a `.then` clause in your Axios request, loop through your five cards. Create `img` tags for each of them, set each `img`'s `src` to a different image URL, and append them to the DOM underneath your `button` tag.

Just like our Dog API project, when you click the button again, it should remove/replace each card with a new card.

## Drawing More or Less Cards

Create a `select` tag underneath your `button`. Your `select` tag should be filled with numbers from 1 through 10. When your user selects a value, you should save their selection in a variable called `numCards`. Instead of drawing five cards each time, use `numCards` to control the number of cards the user draws.

An interesting challenge here for you folks using `replaceChild` for your DOM manipulation - if a user draws five cards, and then draws two cards, how do you ensure that _all five cards_ are removed?

## Styling

It's time to make your browser look like a genuine card table. On your `body`, change the background color to be a medium green. Create a `div` tag to surround your `button`, `select` box, and cards, and make the background color a slightly darker green. Center your cards and inputs on the page, and give them some `padding-top` so that they aren't touching the top of the page directly.

Finally, add a `hover` effect to each card image to make it slightly bigger when the user hovers over it - as if they're selecting that card. Isn't it satisfying to mouse over all your cards now?

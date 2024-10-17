# Prerequisites
- Google Chrome

## Tutorial

- Start by copying the 'main.js' script
- Go to https://twitter.com/
  - Login into your account
- Open the DevTools by pressing Ctrl + Shift + i
- Click on the 'Console' tab
  - Paste the script (we'll come back later to it)
- Click on the 'Network' tab
  - If requests are not being recorded, press CTRL + E and wait 5 seconds
- Click on Fetch/XHR
- You'll see a list of requests, click twice on the 'client_event.json'
- Scroll down and copy the value of the following fields on notepad:
  - Authorization
  - X-Client-Transaction-Id
- Go to the 'Application' tab
  - Cookies
  - Copy the value from the 'guest_id' field
- Go back to the 'Console' tab
- Replace the following field values with the ones you've copied so far
  - var authorization = (replace the * with the Authorization)
  - var client_tid (replace by the X-Client-Transaction-Id)
  - var client_uuid (replace this by the guest_id)
  - var username (your twitter username)
- Press 'Enter' to run the script
- When the deletion it's complete it should appear written on the console the following message: Deletion Complete, to see the results just refresh the page.

## Filtering / Options

- By default the script removes replies and media, if you want to remove retweets as well just change the 'unretweet from false to true.

- You can now choose to delete only tweets that are within a specific date range. For this, edit "before_date" and "after_date" in the `delete_options` variable. These will look like that :
```
	"after_date":new Date('1900-01-01'), // year-month-day
	"before_date":new Date('2100-01-01') // year-month-day
```
Say you want to delete tweets that happened on July 3rd 2023. You would set the date to that :
```
	"after_date":new Date('2023-07-02'), // year-month-day
	"before_date":new Date('2023-07-04') // year-month-day
```
It means : Delete tweet AFTER July 2nd 2023, and BEFORE July 4th 2023. These two dates are not included, so it's only what's in-between these dates, and what's before 2nd and 4th, you got it, 3rd.
NOTE: This is not optimized at all. Meaning the script will go through ALL of your tweets no matter what date you gave. It will only delete tweets that are in the date range you gave, but it will go through all tweets. I will try to optimize it later.

- You can filter which tweets to delete by editing the `delete_options` variable. For now you can decide to remove tweet that contain a certain keyword. For example if you want to delete tweets that contain the word "Hi" or "Hello"(case sensitive), change the variable to look like that :
```
var delete_options = {
	"delete_message_with_url_only":false,
	"match_any_keywords":["Hi", "Hello"]
}
```
- You can also choose to remove tweets only if they contain a link in them. Just change `delete_message_with_url_only` to `true`. You can combine this option with the keywords option.

## Uncaught TypeError: entries is not iterable

If you have this error, in the script edit the random_resource variable from
`var random_resource = "uYU5M2i12UhDvDTzN6hZPg";`
to
`var random_resource = "Q6aAvPw7azXZbqXzuqTALA";`

Then go to the fetch_tweets() function and change the feature variable to:
```
var feature = `&features=%7B%22responsive_web_graphql_exclude_directive_enabled%22%3Atrue%2C%22verified_phone_label_enabled%22%3Afalse%2C%22creator_subscriptions_tweet_preview_api_enabled%22%3Atrue%2C%22responsive_web_graphql_timeline_navigation_enabled%22%3Atrue%2C%22responsive_web_graphql_skip_user_profile_image_extensions_enabled%22%3Afalse%2C%22tweetypie_unmention_optimization_enabled%22%3Atrue%2C%22responsive_web_edit_tweet_api_enabled%22%3Atrue%2C%22graphql_is_translatable_rweb_tweet_is_translatable_enabled%22%3Atrue%2C%22view_counts_everywhere_api_enabled%22%3Atrue%2C%22longform_notetweets_consumption_enabled%22%3Atrue%2C%22responsive_web_twitter_article_tweet_consumption_enabled%22%3Afalse%2C%22tweet_awards_web_tipping_enabled%22%3Afalse%2C%22freedom_of_speech_not_reach_fetch_enabled%22%3Atrue%2C%22standardized_nudges_misinfo%22%3Atrue%2C%22tweet_with_visibility_results_prefer_gql_limited_actions_policy_enabled%22%3Atrue%2C%22longform_notetweets_rich_text_read_enabled%22%3Atrue%2C%22longform_notetweets_inline_media_enabled%22%3Atrue%2C%22responsive_web_media_download_video_enabled%22%3Afalse%2C%22responsive_web_enhance_cards_enabled%22%3Afalse%7D"`
```

## Observations

I'm not the original programmer of this project, I've merely forked the project to improve the tutorial, and something that I've observed it's that this script doesn't remove/delete your likes. I was able to remove all my tweets on one go but if there are leftovers just run the script a second time.

The script still works and i think it's useful for anyone leaving twitter or that doesn't want to have their content used by AI.

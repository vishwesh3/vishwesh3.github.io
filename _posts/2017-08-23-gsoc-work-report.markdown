---
title: "[Draft] GSoC '17 Summary: Improve zulip-mobile"
layout: post
date: 2017-08-23 10:21
image: /assets/images/gsco_banner.png
headerImage: true
tag:
- gsoc
- work report
category: blog
star: true
author: vishwesh
description: Work report for GSoC'17 @zulip
---

My proposal for Improve, enhance current React Native app was selected for Google Summer of Code 2017. I worked with the organisation [Zulip](https://zulipchat.com).

The following sections summarise all my PR's and learnings.

- Don'tshowtick/doneiconifrealmisloggedout. #556 merged
- Handle narrow to unsubscribed stream. #564
- Show smart placeholder for compose input. #599 merged
- Improves login flow. #511
- Learned more about writing tests for functions, components etc, Jest
- fix: app crash on sending PM notification bouncer. #498 merged (on [zulip-android](https://github.com/zulip/zulip-android))
- fix: Autocomplete not being displayed. #611 merged
- Hide soft keyboard on form submission. Submit form with done button in keyboard #483 (merged)
- Make autocomplete suggestions scrollable. #627 merged
- Fix: Line shown when no # stream suggestion matches. #622
- Added clear button to clear search query. #629 merged
- Done testing on iOS, Android 4.1.1, 4.2.2, 4.3, 4.4.4, 5.0.
- Make links and #streams clickable in messages. #639 merged
- Apply bold, italic, links, strikethrough styles in messages. #644
- Show edited tag if messages are edited. #645
- [WIP] Emoji Picker. #646
- Fix: error on message long press in messageSearchScreen. #655 merged
- Improvement in messageActionSheet #658
- Restore theme after closing/reopening the app. #506 (on zulip-android)
- Make message text color to black on Android. #663 merged
- Added share option in messageActionSheet. #668 needs review
- Open link in customTabs on Android. #670 merged
- Use custom tabs to open links on Android (like FB messenger, FB, twitter etc). #669 merged
- [WIP] Add share with/to feature. #674
- Open SubscriptionsScreen on clicking All Streams in left drawer. #681 merged
- Focus compose text after selecting reply. #686
- Added Hindi translations in mobile.json on Transifex
- Do not dismiss keyboard on clicking auto complete row.#695 merged
- Highlight searched text with yellow color. #697 merged
- Replaced TextInput with Input in StreamBox. #708 not required
- Better logic to determine whether message is starred or not. #714 merged
- Added star/unstar option in messageActionSheet. #715 merged
- Written blog on **What are linters?**
- Extracted auto complete pop up from ComposeText. #717 needs review
- Search by initials and in email for people auto complete suggestions. #718
- Handle realm emojis. #723 merged
- Fix: 'undefined is not an object' in message search screen.#732 merged
- Handle stream create, delete, update, occupy events.#730 merged
- Ensure stream is valid before narrowing to it from link in messages. #735
- Handle narrow to unsubscribed stream. #736 merged
- Better handling of EVENT_MESSAGE_UPDATE. #752 merged
- Prioritizes people autocomplete suggestions #762
- [Android] Fix: messageList not displayed when keyboard pops up in SearchMessage Screen. #772 merged
- Fix: email not visible in autocomplete on smaller devices.#776 merged
- Added support of rendering math, mi, mn, math, mrow tags. #780 merged
- fix: splitting message content in several lines. #790 merged
- Added CSS styles for code rendering. #798 merged
- Split class based and tag based text styles. #803 merged
- fix: overlapping of forgot password and google button.#811 merged
- Added Group Details Screen. #821 merged
- Better code formatting #834 merged
- Fix: @mention suggestions disappear after typing a space.#839 merged
- Use actions object to get loginSuccess method in DevAuthScreen. #840 merged
- Added null object constants. #852 merged
- PR fix: jest errors. #858 merged
- Added mfrac tag to render fractions in messages. #866 merged
- No need to show action sheet on long press privateMessageHeader. #868 merged
- Replaced maps with FlatList in AccountPickScreen. #869 merged
- FIx: error on message long press. #870
- Converted isSubscribed() function in Chat.js to a selector.#874 merged
- Initial Implementation of Sentry. #881 merged
- Filter deactivated users from UserScreen and PeopleAutocomplete. #889 merged
- Disable switch in Subscription screen for private stream which is not subscribed. #888 merged
- Fix: undefined error on toggling subscribe switch in subsriptionsScreen. #887 merged
- Fix Android, iOS build. fix Sentry config to upload source map. #891 merged
- fix: error on clicking switch account button. #894 merged
- Fix: headers not being shown in user screen. #900 merged
- Fix: undefined stream name in Lightbox. #901 merged
- Show user status in UserScreen, PeopleAutocomplete and right drawer. #897 needs review => merged
- Created selector to get subscribed streams. #911 merged
- Fix: center align of quote text and bullets. #923 merged
- fix: only active status is shown in UserStatusIndicator. #930
- Renamed mentioned to mentions. #937 merged
- Apply 'user-mention-me' styles to self mentions span. #938
- Handle alert_words events and fetch them in rest of initial data. #957 merged
- fix: mute topics are not updated on events. #959 merged
- Use precise distributor for travis build. #958 merged
- Translated some strings on Transifex in django.po and mobile.json
- Fix: Android crash on entering realm url without protocol. #963 merged
- Change sort order of streams list to match Zulip's standards. #969 merged
- Initial implementation of stream settings. #975
- Added Muted Topic screen in Setting Detail Screen. #982
- Created Alert words screen in Setting details screen. #986
- Fix: autocomplete not being visible on current master.#989 merged
- Fix: status bar style in dark theme for private narrow.#1004 merged
- Better handling of create button in create group screen.#1013 another better one got merged
- fix: message longPress not working. #1018 merged
- Improve options selections in messageActionSheet. #1020 merged
- Fix message editing. #1026 merged
- Fix Status bar style issue in default theme. #1038
- Fix: Compose menu action sheet not visible in Android.#1045
- Fix: message long press not working. #1047 merged
- Fix text not visible in Input/MultilineInput ComposeBox #1046 merged
- Fix: list inside list message rendering. #1063 merged
- Fix: warnings on clicking Add new Account button. #1069 merged
- Fix: UserStatusIndicator not visible. #1071 merged
- Rework on getAutocompletedText. #1078 merged

###Conclusion

It was a great experience working for four months in my GSoC project under [Zulip](https://zulipchat.com). Thanks Zulip community for your guidance and support. Thanks [Google](https://summerofcode.withgoogle.com) and [Zulip](https://zulipchat.com) for giving us this opportunity. 😄

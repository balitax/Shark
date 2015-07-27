# Shark
Swift CLI to transform the .xcassets folder into a type safe enum

### Warning:
Shark is still in development and not ready for production use. I'm still looking for ways to make the setup easier.

**I would love your ideas, feedback, experience about building something like this. Please reach out!**

###How to run:

- Switch to Xcode Beta toolchain - `sudo xcode-select -switch /Applications/Xcode-beta.app/Contents/Developer/`
- cd to the directory where Shark is located

There are 2 ways to run:

1. `swift Shark.swift [PATH-TO-IMAGEASSETS-FOLDER] [OUTPUT-DIRECTORY]`

Example:
```bash 
swift Shark.swift ~/Code/Noluyo/Noluyo/Images.xcassets/ ~/Desktop
```
 
**OR**

2. move shark executable to /usr/local/bin and call `shark [PATH-TO-IMAGEASSETS-FOLDER] [OUTPUT-DIRECTORY]`


###How to Build an executable:
 `xcrun -sdk macosx swiftc Shark.swift -o shark`

---

In the future, we will try to distribute Shark with homebrew to make installation/usage easier.

---

Here's an example output

```swift 
//SharkImageNames.swift
//Generated by Shark

public protocol SharkImageConvertible {}

public extension SharkImageConvertible where Self: RawRepresentable, Self.RawValue == String {
    public var image: UIImage? {
        return UIImage(named: self.rawValue)
    }
}

public extension UIImage {
    convenience init?<T: RawRepresentable where T.RawValue == String>(shark: T) {
        self.init(named: shark.rawValue)
    }
}

public enum Shark: String, SharkImageConvertible {

    public enum EmptyIcons: String, SharkImageConvertible {
            case feed_empty_icon
            case news_empty_icon
            case programs_empty_icon
            case reminders_empty_icon
            case watch_list_empty_icon
    }

        case badge_locked
        case comment-count-icon
        case delete_account_icon
        case checkbox-icon
        case end-of-feed-icon
        case facebook-icon
        case facebook-share-checked
        case facebook-share-unchecked
        case feed-view-like-icon-checked
        case feed-view-like-icon-unchecked
        case feed-view-post-follow-icon
        case feed-view-post-link-icon
        case feed-view-share-icon
        case follow-icon-checked
        case follow-icon-unchecked
        case hamburger-menu-icon
        case logout_icon
        case media-icon-checked
        case media-icon-unchecked
        case nav-back-icon
        case nav-forward-icon
        case new-post-icon
        case news-filter-confirm
        case noluyo_logo
        case NoluyoTitleText
        case post-media-delete-icon
        case post_delete_icon
        case profile-icon-programs
        case profile-reminders-delete-icon
        case profile_placeholder
        case program_badge_icon
        case program_feed_icon
        case program_game_icon
        case program_schedule_icon
        case program_watching_eye
        case rating-star-checked
        case rating-star-unchecked
        case register_add_image
        case reminder-icon-checked
        case reminder-icon-unchecked
        case report-icon
        case search-icon
        case show-episode-iist-icon
        case show-follower-icon
        case show-more-info-icon
        case show-news-filter-facebook-icon-checked
        case show-news-filter-facebook-icon-unchecked
        case show-news-filter-facebook-icon
        case show-news-filter-icon
        case show-news-filter-instagram-icon-checked
        case show-news-filter-instagram-icon-unchecked
        case show-news-filter-noluyo-icon-checked
        case show-news-filter-noluyo-icon-unchecked
        case show-news-filter-noluyo-icon
        case show-news-filter-twitter-icon-checked
        case show-news-filter-twitter-icon-unchecked
        case show-news-filter-twitter-icon
        case show-now-icon
        case show-share-icon
        case show-trending-icon
        case side-menu-discover-icon
        case side-menu-light
        case side-menu-line
        case side-menu-news-icon
        case side-menu-notifications-icon
        case side-menu-settings-icon
        case side-menu-tvguide-icon
        case side-menu-watchlist-icon
        case suggestion-follower-icon
        case suggestion-view-icon
        case tag-icon-checked
        case tag-icon-unchecked
        case tag-search-livenow-icon-checked
        case tag-search-livenow-icon-unchecked
        case tag-search-trending-icon-checked
        case tag-search-trending-icon-unchecked
        case trophies-list-icon
        case trophy-badge-icon
        case tumblr-icon
        case tumblr-share-checked
        case tumblr-share-unchecked
        case tv-guide-fiter-icon
        case tv-guide-now-button
        case tv_guide_back_arrow
        case tv_guide_filter_delete_button
        case tv_guide_filter_down_arrow
        case tv_guide_forward_arrow
        case twitter-icon
        case twitter-share-checked
        case twitter-share-unchecked
        case video-feed-play-icon
        case watchlist-checked-icon
        case watchlist-down-arrow
        case watchlist-unchecked-icon
        case feed-view-post-watch-icon
}
```

With this, we can get type-safe images in two ways

```swift
myImageView.image = UIImage(shark: Shark.EmptyIcons.programs_empty_icon)
```
**OR**
```swift
myImageView.image = Shark.EmptyIcons.programs_empty_icon.image
```


##To-Do
- [ ] Add example project
- [ ] Homebrew Support
- [ ] Cocoapods Support to automatically add Shark - Pre-build script to the Xcode Project
- [ ] Handle Multiple .imageAssets folders in a single project
- [ ] Clean up


##License
The MIT License (MIT)

Copyright (c) 2015 Kaan Dedeoglu

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

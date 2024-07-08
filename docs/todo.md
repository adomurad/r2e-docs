---
sidebar_position: 6
---

# TODO

There are still many **webdriver** capabilities not implemented yet.

Here is a simplified spec: [https://github.com/jlipps/simple-wd-spec/](https://github.com/jlipps/simple-wd-spec/)

## Implementation Progress

The **R2E** api is not the same as webdriver's - but this table at least tracks what capabilities are still missing.

| Method | URI Template                                                         | Command                                                   | Done |
| ------ | -------------------------------------------------------------------- | --------------------------------------------------------- | ---- |
| POST   | /session                                                             | [New Session](#new-session)                               | ✅   |
| DELETE | /session/\{session id\}                                              | [Delete Session](#delete-session)                         | ✅   |
| GET    | /status                                                              | [Status](#status)                                         | ✅   |
| GET    | /session/\{session id\}/timeouts                                     | [Get Timeouts](#get-timeouts)                             | ❌   |
| POST   | /session/\{session id\}/timeouts                                     | [Set Timeouts](#set-timeouts)                             | ❌   |
| POST   | /session/\{session id\}/url                                          | [Go](#go)                                                 | ✅   |
| GET    | /session/\{session id\}/url                                          | [Get Current URL](#get-current-url)                       | ✅   |
| POST   | /session/\{session id\}/back                                         | [Back](#back)                                             | ✅   |
| POST   | /session/\{session id\}/forward                                      | [Forward](#forward)                                       | ✅   |
| POST   | /session/\{session id\}/refresh                                      | [Refresh](#refresh)                                       | ✅   |
| GET    | /session/\{session id\}/title                                        | [Get Title](#get-title)                                   | ✅   |
| GET    | /session/\{session id\}/window                                       | [Get Window Handle](#get-window-handle)                   | ❌   |
| DELETE | /session/\{session id\}/window                                       | [Close Window](#close-window)                             | ❌   |
| POST   | /session/\{session id\}/window                                       | [Switch To Window](#switch-to-window)                     | ❌   |
| GET    | /session/\{session id\}/window/handles                               | [Get Window Handles](#get-window-handles)                 | ❌   |
| POST   | /session/\{session id\}/frame                                        | [Switch To Frame](#switch-to-frame)                       | ❌   |
| POST   | /session/\{session id\}/frame/parent                                 | [Switch To Parent Frame](#switch-to-parent-frame)         | ❌   |
| GET    | /session/\{session id\}/window/rect                                  | [Get Window Rect](#get-window-rect)                       | ✅   |
| POST   | /session/\{session id\}/window/rect                                  | [Set Window Rect](#set-window-rect)                       | ✅   |
| POST   | /session/\{session id\}/window/maximize                              | [Maximize Window](#maximize-window)                       | ✅   |
| POST   | /session/\{session id\}/window/minimize                              | [Minimize Window](#minimize-window)                       | ✅   |
| POST   | /session/\{session id\}/window/fullscreen                            | [Fullscreen Window](#fullscreen-window)                   | ✅   |
| POST   | /session/\{session id\}/element                                      | [Find Element](#find-element)                             | ✅   |
| POST   | /session/\{session id\}/elements                                     | [Find Elements](#find-elements)                           | ✅   |
| POST   | /session/\{session id\}/element/\{element id\}/element               | [Find Element From Element](#find-element-from-element)   | ❌   |
| POST   | /session/\{session id\}/element/\{element id\}/elements              | [Find Elements From Element](#find-elements-from-element) | ❌   |
| GET    | /session/\{session id\}/element/active                               | [Get Active Element](#get-active-element)                 | ❌   |
| GET    | /session/\{session id\}/element/\{element id\}/selected              | [Is Element Selected](#is-element-selected)               | ❌   |
| GET    | /session/\{session id\}/element/\{element id\}/attribute/\{name\}    | [Get Element Attribute](#get-element-attribute)           | ✅   |
| GET    | /session/\{session id\}/element/\{element id\}/property/\{name\}     | [Get Element Property](#get-element-property)             | ✅   |
| GET    | /session/\{session id\}/element/\{element id\}/css/\{property name\} | [Get Element CSS Value](#get-element-css-value)           | ❌   |
| GET    | /session/\{session id\}/element/\{element id\}/text                  | [Get Element Text](#get-element-text)                     | ✅   |
| GET    | /session/\{session id\}/element/\{element id\}/name                  | [Get Element Tag Name](#get-element-tag-name)             | ❌   |
| GET    | /session/\{session id\}/element/\{element id\}/rect                  | [Get Element Rect](#get-element-rect)                     | ❌   |
| GET    | /session/\{session id\}/element/\{element id\}/enabled               | [Is Element Enabled](#is-element-enabled)                 | ❌   |
| POST   | /session/\{session id\}/element/\{element id\}/click                 | [Element Click](#element-click)                           | ✅   |
| POST   | /session/\{session id\}/element/\{element id\}/clear                 | [Element Clear](#element-clear)                           | ✅   |
| POST   | /session/\{session id\}/element/\{element id\}/value                 | [Element Send Keys](#element-send-keys)                   | ✅   |
| GET    | /session/\{session id\}/source                                       | [Get Page Source](#get-page-source)                       | ❌   |
| POST   | /session/\{session id\}/execute/sync                                 | [Execute Script](#execute-script)                         | ❌   |
| POST   | /session/\{session id\}/execute/async                                | [Execute Async Script](#execute-async-script)             | ❌   |
| GET    | /session/\{session id\}/cookie                                       | [Get All Cookies](#get-all-cookies)                       | ❌   |
| GET    | /session/\{session id\}/cookie/\{name\}                              | [Get Named Cookie](#get-named-cookie)                     | ❌   |
| POST   | /session/\{session id\}/cookie                                       | [Add Cookie](#add-cookie)                                 | ❌   |
| DELETE | /session/\{session id\}/cookie/\{name\}                              | [Delete Cookie](#delete-cookie)                           | ❌   |
| DELETE | /session/\{session id\}/cookie                                       | [Delete All Cookies](#delete-all-cookies)                 | ❌   |
| POST   | /session/\{session id\}/actions                                      | [Perform Actions](#perform-actions)                       | ❌   |
| DELETE | /session/\{session id\}/actions                                      | [Release Actions](#release-actions)                       | ❌   |
| POST   | /session/\{session id\}/alert/dismiss                                | [Dismiss Alert](#dismiss-alert)                           | ❌   |
| POST   | /session/\{session id\}/alert/accept                                 | [Accept Alert](#accept-alert)                             | ❌   |
| GET    | /session/\{session id\}/alert/text                                   | [Get Alert Text](#get-alert-text)                         | ❌   |
| POST   | /session/\{session id\}/alert/text                                   | [Send Alert Text](#send-alert-text)                       | ❌   |
| GET    | /session/\{session id\}/screenshot                                   | [Take Screenshot](#take-screenshot)                       | ⚠️   |
| GET    | /session/\{session id\}/element/\{element id\}/screenshot            | [Take Element Screenshot](#take-element-screenshot)       | ⚠️   |
| POST   | /session/\{session id\}/print                                        | [Print Page](#print-page)                                 | ⚠️   |

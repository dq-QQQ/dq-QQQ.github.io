---
title: iOS의 빌드세팅
date: 2025-11-27
excerpt: "Xcode에서 빌드세팅목록"
categories:
- iOS
tags:
- iOS-PRO
---


<br />
<br />

---

# 개요

---

값 하나때문에 되고 안되고 으아아!!!!



<br />

---

# 


[DEBUG_CALLSTACK | GetInformation-2026-02-05 08:44:07.949 | CURRENT_PAGE] 호출 시점 로그: 
0   OZRViewer                           0x000000010b902000 -[OZReportViewerImpl GetInformation:] + 200
1   FPPlanner_QA.debug.dylib            0x000000010584a6a4 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
2   FPPlanner_QA.debug.dylib            0x0000000105848cfc $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
3   FPPlanner_QA.debug.dylib            0x000000010584849c $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
4   FPPlanner_QA.debug.dylib            0x0000000105849414 $s12FPPlanner_QA25SSPESubSignViewControllerC011userCon
tentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
5   WebKit                              0x0000




[DEBUG_CALLSTACK | GetInformation-2026-02-05 08:44:07.976 | CURRENT_PAGE] 호출 시점 로그: 
0   OZRViewer                           0x000000010b902000 -[OZReportViewerImpl GetInformation:] + 200
1   FPPlanner_QA.debug.dylib            0x000000010584a6a4 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
2   FPPlanner_QA.debug.dylib            0x0000000105848cfc $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
3   FPPlanner_QA.debug.dylib            0x000000010584849c $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
4   FPPlanner_QA.debug.dylib            0x0000000105849414 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
5   WebKit                              0x0000




[DEBUG_CALLSTACK | GetInformation-2026-02-05 08:44:07.993 | INPUT_CHECK_VALIDITY_PAGE_AT=4] 호출 시점 로그: 
0   OZRViewer                           0x000000010b902000 -[OZReportViewerImpl GetInformation:] + 200
1   FPPlanner_QA.debug.dylib            0x000000010584a6a4 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
2   FPPlanner_QA.debug.dylib            0x0000000105848cfc $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
3   FPPlanner_QA.debug.dylib            0x000000010584849c $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
4   FPPlanner_QA.debug.dylib            0x0000000105849414 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
5   WebKit




[DEBUG_CALLSTACK | Flush doc: 0 page: 3 | 2026-02-05 08:44:07.996] 호출 시점 로그: 
0   OZRViewer                           0x000000010b8824f4 -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 136
1   OZRViewer                           0x000000010b6dbef8 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
2   OZRViewer                           0x000000010b4327a0 _ZN18OZCViewerReportDoc15OnCheckValidityEP7OZCPage + 212
3   OZRViewer                           0x000000010b8274ec _ZN12OZCMainFrame14GetInformationE7CString + 22228
4   OZRViewer                           0x000000010b9020e0 -[OZReportViewerImpl GetInformation:] + 424
5   FPPlanner_QA.debug.dylib            0x000000010584a6a4 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
6   FPPlanner_QA.debug.dylib            0x0000000105848cfc $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D






[DEBUG_CALLSTACK | Close Sign-2026-02-05 08:44:08.000 | <XSignButton: 0x13a074400; frame = (132.661 3295.22; 82.205 18.1421); userInteractionEnabled = NO; backgroundColor = UIExtendedGrayColorSpace 0 0; layer = <CALayer: 0x13a241240>>] 호출 시점 로그: 
0   OZRViewer                           0x000000010ba50650 -[XSignButton closeUI:] + 196
1   OZRViewer                           0x000000010ba50f2c -[XSignButton closeDialogUI:] + 112
2   OZRViewer                           0x000000010ba51044 -[XSignButton resignFirstResponder] + 248
3   OZRViewer                           0x000000010b88215c -[XReportView resignFirstResponderForSubviews:docIndex:pageIndex:] + 1556
4   OZRViewer                           0x000000010b8828fc -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 1168
5   OZRViewer                           0x000000010b6dbef8 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
6   OZRViewer                           0x000000010b4327a0 _ZN18OZCViewerReportDoc15OnCheckValidityEP7O






[DEBUG_CALLSTACK | Close Sign-2026-02-05 08:44:08.009 | <XSignButton: 0x1198b2000; frame = (216 3295.22; 82.205 18.1421); userInteractionEnabled = NO; backgroundColor = UIExtendedGrayColorSpace 0 0; layer = <CALayer: 0x13a2404c0>>] 호출 시점 로그: 
0   OZRViewer                           0x000000010ba50650 -[XSignButton closeUI:] + 196
1   OZRViewer                           0x000000010ba50f2c -[XSignButton closeDialogUI:] + 112
2   OZRViewer                           0x000000010ba51044 -[XSignButton resignFirstResponder] + 248
3   OZRViewer                           0x000000010b88215c -[XReportView resignFirstResponderForSubviews:docIndex:pageIndex:] + 1556
4   OZRViewer                           0x000000010b8828fc -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 1168
5   OZRViewer                           0x000000010b6dbef8 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
6   OZRViewer                           0x000000010b4327a0 _ZN18OZCViewerReportDoc15OnCheckValidityEP7OZCPa


















[DEBUG_CALLSTACK | Call OZEFormInputEventCommand-2026-02-10 09:14:14.467 0 C0400_hss_nm| OnFocus] log: 
0   OZRViewer                           0x0000000109882754 _ZN20OZCommandListenerIOS24OZEFormInputEventCommandEPwS0_S0_S0_ + 160
1   OZRViewer                           0x0000000109b0a218 _ZN18OZCommandInterface28FireOZEFormInputEventCommandEPPwS1_S1_S1_ + 104
2   OZRViewer                           0x0000000109b094d0 _ZN18OZCommandInterface24OZEFormInputEventCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 504
3   OZRViewer                           0x0000000109b06884 _ZN18OZCommandInterface13FireOZCommandEyx + 864
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x000000018360f3d4 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10400724
6   Foundation                          0x000000018360f570 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10401136
7   OZRViewer                           0x0000000109ac29d4 _Z11SendMessagePvjyx + 220
8   OZRViewer                           0x00000001097de184 _ZN16CNotifierToEvent8OZNotifyE7CStringR10OZAtlArrayIS0_15OZElementTraitsIS0_EEbbi + 520
9   OZRViewer                           0x0000000108f71614 _ZN6OZCOne28CallOZEFormInputEventCommandE7CStringi + 732
10  OZRViewer                           0x0000000108f83aa8 _ZN8OZCOneIC7OnFocusEib + 328
11  OZRViewer                           0x0000000109de2450 _ZN16OZInputComponent7OnFocusEv + 148
12  OZRViewer                           0x0000000109bf0554 -[XSignButton onFocus] + 1212
13  OZRViewer                           0x0000000109bee2c4 -[XSignButton becomeFirstResponder:] + 1472
14  OZRViewer                           0x0000000109bedcf8 -[XSignButton becomeFirstResponder] + 36
15  OZRViewer                           0x0000000109bf7bbc -[XSignButton onClicked:] + 3728
16  OZRViewer                           0x0000000109bf185c -[XSignButton onTouchUpInside:] + 268
17  OZRViewer                           0x0000000109a1a480 -[XReportView selectInputComponent:recognizer:isInputMode:fromFixed:] + 3984
18  OZRViewer                           0x0000000109a190b4 -[XReportView onGestureTap:] + 7616
19  UIKitCore                           0x000000018bf3ad1c 48736F98-163C-3430-AC20-54E325234380 + 15899932
20  UIKitCore                           0x000000018b2f9ec8 48736F98-163C-3430-AC20-54E325234380 + 3051208
21  UIKitCore                           0x000000018b2f9c88 48736F98-163C-3430-AC20-54E325234380 + 3050632
22  UIKitCore                           0x000000018b08b20c 48736F98-163C-3430-AC20-54E325234380 + 500236
23  UIKitCore                           0x000000018bf35af8 48736F98-163C-3430-AC20-54E325234380 + 15878904
24  UIKitCore                           0x000000018bf32588 48736F98-163C-3430-AC20-54E325234380 + 15865224
25  CoreFoundation                      0x0000000185644ea0 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 380576
26  CoreFoundation                      0x000000018562e58c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 288140
27  CoreFoundation                      0x0000000185605740 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120640
28  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
29  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
30  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
31  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
32  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
33  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008




[DEBUG_CALLSTACK | Call OZEFormInputEventCommand-2026-02-10 09:14:14.498 0 C0400_hss_sign| OnFocus] log: 
0   OZRViewer                           0x0000000109882754 _ZN20OZCommandListenerIOS24OZEFormInputEventCommandEPwS0_S0_S0_ + 160
1   OZRViewer                           0x0000000109b0a218 _ZN18OZCommandInterface28FireOZEFormInputEventCommandEPPwS1_S1_S1_ + 104
2   OZRViewer                           0x0000000109b094d0 _ZN18OZCommandInterface24OZEFormInputEventCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 504
3   OZRViewer                           0x0000000109b06884 _ZN18OZCommandInterface13FireOZCommandEyx + 864
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x000000018360f3d4 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10400724
6   Foundation                          0x000000018360f570 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10401136
7   OZRViewer                           0x0000000109ac29d4 _Z11SendMessagePvjyx + 220
8   OZRViewer                           0x00000001097de184 _ZN16CNotifierToEvent8OZNotifyE7CStringR10OZAtlArrayIS0_15OZElementTraitsIS0_EEbbi + 520
9   OZRViewer                           0x0000000108f71614 _ZN6OZCOne28CallOZEFormInputEventCommandE7CStringi + 732
10  OZRViewer                           0x0000000108f83aa8 _ZN8OZCOneIC7OnFocusEib + 328
11  OZRViewer                           0x0000000109de2450 _ZN16OZInputComponent7OnFocusEv + 148
12  OZRViewer                           0x0000000109bf0554 -[XSignButton onFocus] + 1212
13  OZRViewer                           0x0000000109bee2c4 -[XSignButton becomeFirstResponder:] + 1472
14  OZRViewer                           0x0000000109bedcf8 -[XSignButton becomeFirstResponder] + 36
15  OZRViewer                           0x0000000109bf7bbc -[XSignButton onClicked:] + 3728
16  OZRViewer                           0x0000000109bf185c -[XSignButton onTouchUpInside:] + 268
17  OZRViewer                           0x0000000109a1a480 -[XReportView selectInputComponent:recognizer:isInputMode:fromFixed:] + 3984
18  OZRViewer                           0x0000000109a190b4 -[XReportView onGestureTap:] + 7616
19  UIKitCore                           0x000000018bf3ad1c 48736F98-163C-3430-AC20-54E325234380 + 15899932
20  UIKitCore                           0x000000018b2f9ec8 48736F98-163C-3430-AC20-54E325234380 + 3051208
21  UIKitCore                           0x000000018b2f9c88 48736F98-163C-3430-AC20-54E325234380 + 3050632
22  UIKitCore                           0x000000018b08b20c 48736F98-163C-3430-AC20-54E325234380 + 500236
23  UIKitCore                           0x000000018bf35af8 48736F98-163C-3430-AC20-54E325234380 + 15878904
24  UIKitCore                           0x000000018bf32588 48736F98-163C-3430-AC20-54E325234380 + 15865224
25  CoreFoundation                      0x0000000185644ea0 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 380576
26  CoreFoundation                      0x000000018562e58c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 288140
27  CoreFoundation                      0x0000000185605740 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120640
28  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
29  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
30  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
31  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
32  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
33  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008





[DEBUG_CALLSTACK | Call OZEFormInputEventCommand-2026-02-10 09:14:14.518 0 C0400_hss_nm| OnClick] log: 
0   OZRViewer                           0x0000000109882754 _ZN20OZCommandListenerIOS24OZEFormInputEventCommandEPwS0_S0_S0_ + 160
1   OZRViewer                           0x0000000109b0a218 _ZN18OZCommandInterface28FireOZEFormInputEventCommandEPPwS1_S1_S1_ + 104
2   OZRViewer                           0x0000000109b094d0 _ZN18OZCommandInterface24OZEFormInputEventCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 504
3   OZRViewer                           0x0000000109b06884 _ZN18OZCommandInterface13FireOZCommandEyx + 864
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x000000018360f3d4 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10400724
6   Foundation                          0x000000018360f570 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10401136
7   OZRViewer                           0x0000000109ac29d4 _Z11SendMessagePvjyx + 220
8   OZRViewer                           0x00000001097de184 _ZN16CNotifierToEvent8OZNotifyE7CStringR10OZAtlArrayIS0_15OZElementTraitsIS0_EEbbi + 520
9   OZRViewer                           0x0000000108f71614 _ZN6OZCOne28CallOZEFormInputEventCommandE7CStringi + 732
10  OZRViewer                           0x0000000108f83920 _ZN8OZCOneIC9OnClickedEi + 268
11  OZRViewer                           0x0000000109bf0770 -[XSignButton onFocus] + 1752
12  OZRViewer                           0x0000000109bee2c4 -[XSignButton becomeFirstResponder:] + 1472
13  OZRViewer                           0x0000000109bedcf8 -[XSignButton becomeFirstResponder] + 36
14  OZRViewer                           0x0000000109bf7bbc -[XSignButton onClicked:] + 3728
15  OZRViewer                           0x0000000109bf185c -[XSignButton onTouchUpInside:] + 268
16  OZRViewer                           0x0000000109a1a480 -[XReportView selectInputComponent:recognizer:isInputMode:fromFixed:] + 3984
17  OZRViewer                           0x0000000109a190b4 -[XReportView onGestureTap:] + 7616
18  UIKitCore                           0x000000018bf3ad1c 48736F98-163C-3430-AC20-54E325234380 + 15899932
19  UIKitCore                           0x000000018b2f9ec8 48736F98-163C-3430-AC20-54E325234380 + 3051208
20  UIKitCore                           0x000000018b2f9c88 48736F98-163C-3430-AC20-54E325234380 + 3050632
21  UIKitCore                           0x000000018b08b20c 48736F98-163C-3430-AC20-54E325234380 + 500236
22  UIKitCore                           0x000000018bf35af8 48736F98-163C-3430-AC20-54E325234380 + 15878904
23  UIKitCore                           0x000000018bf32588 48736F98-163C-3430-AC20-54E325234380 + 15865224
24  CoreFoundation                      0x0000000185644ea0 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 380576
25  CoreFoundation                      0x000000018562e58c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 288140
26  CoreFoundation                      0x0000000185605740 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120640
27  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
28  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
29  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
30  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
31  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
32  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008



[DEBUG_CALLSTACK | SetActiveReport 변경됨
[DEBUG_CALLSTACK | SetActiveReport: 1 | 2026-02-10 09:14:14.538] 호출 시점 로그: 
0   OZRViewer                           0x000000010985bd54 _ZN12OZCMainFrame15SetActiveReportEibbb + 2828
1   OZRViewer                           0x0000000109aa9d88 _ZN17OZCViewerTreeView10SelectNodeEP9XTreeNodeb + 676
2   OZRViewer                           0x0000000109aa9ad8 _ZN17OZCViewerTreeView10SelectItemEi + 84
3   OZRViewer                           0x00000001099dbd94 _ZN12OZCMainFrame14SelectTreeItemEi + 56
4   OZRViewer                           0x000000010980873c _ZN15OZCPagesControl10ChangePageEiibbbbb + 1276
5   OZRViewer                           0x000000010980a79c _ZN15OZCPagesControl10PageMoveToEiibbbbb + 112
6   OZRViewer                           0x0000000109a4cc44 _ZN19OZCViewerReportView23ScrollUpdateCurrentPageEb + 4464
7   OZRViewer                           0x0000000109876c98 _ZN19OZCViewerReportView13SetScrollSizeEb + 888
8   OZRViewer                           0x00000001095c91c8 _ZN18OZCViewerRepo



[DEBUG_CALLSTACK | SetActiveReport: ReportChangeCommand 실행됨
[TRACE] selected: %s
10.28.0 - [FirebaseAnalytics][I-ACS031006] View controller already tracked. Class, ID: SSPESubSignViewController, -7413028598299875770
>>> request drawPageImage: 3 <<<
>>> begin drawPageImage: 3



[DEBUG_CALLSTACK | Call ReportChangeCommand-2026-02-10 09:14:14.554 | 1] log: 
0   OZRViewer                           0x00000001098825a8 _ZN20OZCommandListenerIOS21OZReportChangeCommandEPw + 176
1   OZRViewer                           0x0000000109b0a194 _ZN18OZCommandInterface25FireOZReportChangeCommandEPPw + 68
2   OZRViewer                           0x0000000109b091e4 _ZN18OZCommandInterface21OZReportChangeCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 120
3   OZRViewer                           0x0000000109b0684c _ZN18OZCommandInterface13FireOZCommandEyx + 808
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x0000000182c601d0 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 246224
6   CoreFoundation                      0x0000000185650f10 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429840
7   CoreFoundation                      0x0000000185650e84 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429700
8   CoreFoundation                      0x000000018562eb30 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 289584
9   CoreFoundation                      0x00000001856056d8 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120536
10  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
11  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
12  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
13  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
14  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
15  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008





[DEBUG_CALLSTACK | Call OZPageChangeCommand-2026-02-10 09:14:14.557 | 1] log: 
0   OZRViewer                           0x00000001098822d4 _ZN20OZCommandListenerIOS19OZPageChangeCommandEPw + 176
1   OZRViewer                           0x0000000109b0a0bc _ZN18OZCommandInterface23FireOZPageChangeCommandEPPw + 68
2   OZRViewer                           0x0000000109b08e64 _ZN18OZCommandInterface19OZPageChangeCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 92
3   OZRViewer                           0x0000000109b067dc _ZN18OZCommandInterface13FireOZCommandEyx + 696
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x0000000182c601d0 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 246224
6   CoreFoundation                      0x0000000185650f10 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429840
7   CoreFoundation                      0x0000000185650e84 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429700
8   CoreFoundation                      0x000000018562eb30 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 289584
9   CoreFoundation                      0x00000001856056d8 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120536
10  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
11  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
12  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
13  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
14  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
15  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008










[DEBUG_CALLSTACK | GetInformation-2026-02-10 09:14:14.677 | CURRENT_PAGE] 호출 시점 로그: 
0   OZRViewer                           0x0000000109a9e4ec -[OZReportViewerImpl GetInformation:] + 200
1   FPPlanner_QA.debug.dylib            0x00000001039e65a8 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
2   FPPlanner_QA.debug.dylib            0x00000001039e4c00 $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
3   FPPlanner_QA.debug.dylib            0x00000001039e43a0 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
4   FPPlanner_QA.debug.dylib            0x00000001039e5318 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
5   WebKit                              0x0000










[DEBUG_CALLSTACK | GetInformation-2026-02-10 09:14:14.685 | INPUT_CHECK_VALIDITY_PAGE_AT=4] 호출 시점 로그: 
0   OZRViewer                           0x0000000109a9e4ec -[OZReportViewerImpl GetInformation:] + 200
1   FPPlanner_QA.debug.dylib            0x00000001039e65a8 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
2   FPPlanner_QA.debug.dylib            0x00000001039e4c00 $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
3   FPPlanner_QA.debug.dylib            0x00000001039e43a0 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
4   FPPlanner_QA.debug.dylib            0x00000001039e5318 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
5   WebKit










[DEBUG_CALLSTACK | Flush doc: 0 page: 3 | 2026-02-10 09:14:14.688] 호출 시점 로그: 
0   OZRViewer                           0x0000000109a1e96c -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 136
1   OZRViewer                           0x0000000109877fe0 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
2   OZRViewer                           0x00000001095ce76c _ZN18OZCViewerReportDoc15OnCheckValidityEP7OZCPage + 212
3   OZRViewer                           0x00000001099c3950 _ZN12OZCMainFrame14GetInformationE7CString + 22228
4   OZRViewer                           0x0000000109a9e5cc -[OZReportViewerImpl GetInformation:] + 424
5   FPPlanner_QA.debug.dylib            0x00000001039e65a8 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
6   FPPlanner_QA.debug.dylib            0x00000001039e4c00 $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D






[DEBUG_CALLSTACK | Close Sign-2026-02-10 09:14:14.693 | <XSignButton: 0x14b983400; frame = (132.661 3295.22; 82.205 18.1421); userInteractionEnabled = NO; backgroundColor = UIExtendedGrayColorSpace 0 0; layer = <CALayer: 0x10bd99fe0>>] 호출 시점 로그: 
0   OZRViewer                           0x0000000109becb3c -[XSignButton closeUI:] + 196
1   OZRViewer                           0x0000000109bed418 -[XSignButton closeDialogUI:] + 112
2   OZRViewer                           0x0000000109bed530 -[XSignButton resignFirstResponder] + 248
3   OZRViewer                           0x0000000109a1e5d4 -[XReportView resignFirstResponderForSubviews:docIndex:pageIndex:] + 1556
4   OZRViewer                           0x0000000109a1ed74 -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 1168
5   OZRViewer                           0x0000000109877fe0 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
6   OZRViewer                           0x00000001095ce76c _ZN18OZCViewerReportDoc15OnCheckValidityEP7O












[DEBUG_CALLSTACK | Call OZEFormInputEventCommand-2026-02-10 09:14:14.700 0 C0400_hss_nm| OnKillFocus] log: 
0   OZRViewer                           0x0000000109882754 _ZN20OZCommandListenerIOS24OZEFormInputEventCommandEPwS0_S0_S0_ + 160
1   OZRViewer                           0x0000000109b0a218 _ZN18OZCommandInterface28FireOZEFormInputEventCommandEPPwS1_S1_S1_ + 104
2   OZRViewer                           0x0000000109b094d0 _ZN18OZCommandInterface24OZEFormInputEventCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 504
3   OZRViewer                           0x0000000109b06884 _ZN18OZCommandInterface13FireOZCommandEyx + 864
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x000000018360f3d4 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10400724
6   Foundation                          0x000000018360f570 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10401136
7   OZRViewer                           0x0000000109ac29d4 _Z11SendMessagePvjyx + 220
8   OZRViewer                           0x00000001097de184 _ZN16CNotifierToEvent8OZNotifyE7CStringR10OZAtlArrayIS0_15OZElementTraitsIS0_EEbbi + 520
9   OZRViewer                           0x0000000108f71614 _ZN6OZCOne28CallOZEFormInputEventCommandE7CStringi + 732
10  OZRViewer                           0x0000000108f83bd8 _ZN8OZCOneIC11OnKillFocusEib + 244
11  OZRViewer                           0x0000000109de2568 _ZN16OZInputComponent11OnKillFocusEv + 144
12  OZRViewer                           0x0000000109bf0904 -[XSignButton onKillFocus] + 300
13  OZRViewer                           0x0000000109bed06c -[XSignButton closeUI:] + 1524
14  OZRViewer                           0x0000000109bed418 -[XSignButton closeDialogUI:] + 112
15  OZRViewer                           0x0000000109bed530 -[XSignButton resignFirstResponder] + 248
16  OZRViewer                           0x0000000109a1e5d4 -[XReportView resignFirstResponderForSubviews:docIndex:pageIndex:] + 1556
17  OZRViewer                           0x0000000109a1ed74 -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 1168
18  OZRViewer                           0x0000000109877fe0 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
19  OZRViewer                           0x00000001095ce76c _ZN18OZCViewerReportDoc15OnCheckValidityEP7OZCPage + 212
20  OZRViewer                           0x00000001099c3950 _ZN12OZCMainFrame14GetInformationE7CString + 22228
21  OZRViewer                           0x0000000109a9e5cc -[OZReportViewerImpl GetInformation:] + 424
22  FPPlanner_QA.debug.dylib            0x00000001039e65a8 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
23  FPPlanner_QA.debug.dylib            0x00000001039e4c00 $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
24  FPPlanner_QA.debug.dylib            0x00000001039e43a0 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
25  FPPlanner_QA.debug.dylib            0x00000001039e5318 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
26  WebKit                              0x00000001a0d13674 9B408D7C-337B-3328-8A80-C331F371C59D + 7464564
27  WebKit                              0x00000001a13c2dd8 9B408D7C-337B-3328-8A80-C331F371C59D + 14474712
28  WebKit                              0x00000001a12f5370 9B408D7C-337B-3328-8A80-C331F371C59D + 13632368
29  WebKit                              0x00000001a068a330 9B408D7C-337B-3328-8A80-C331F371C59D + 611120
30  WebKit                              0x00000001a0678234 9B408D7C-337B-3328-8A80-C331F371C59D + 537140
31  WebKit                              0x00000001a0687e18 9B408D7C-337B-3328-8A80-C331F371C59D + 601624
32  JavaScriptCore                      0x000000019b22988c D72A92C4-12ED-3239-9568-8950D3DE8B76 + 1575052
33  JavaScriptCore                      0x000000019b229644 D72A92C4-12ED-3239-9568-8950D3DE8B76 + 1574468
34  CoreFoundation                      0x0000000185650f10 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429840
35  CoreFoundation                      0x0000000185650e84 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429700
36  CoreFoundation                      0x000000018562eb30 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 289584
37  CoreFoundation                      0x00000001856056d8 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120536
38  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
39  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
40  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
41  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
42  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
43  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008






[DEBUG_CALLSTACK | Call OZEFormInputEventCommand-2026-02-10 09:14:14.711 0 C0400_hss_sign| OnKillFocus] log: 
0   OZRViewer                           0x0000000109882754 _ZN20OZCommandListenerIOS24OZEFormInputEventCommandEPwS0_S0_S0_ + 160
1   OZRViewer                           0x0000000109b0a218 _ZN18OZCommandInterface28FireOZEFormInputEventCommandEPPwS1_S1_S1_ + 104
2   OZRViewer                           0x0000000109b094d0 _ZN18OZCommandInterface24OZEFormInputEventCommandER10OZAtlArrayI7CString15OZElementTraitsIS1_EE + 504
3   OZRViewer                           0x0000000109b06884 _ZN18OZCommandInterface13FireOZCommandEyx + 864
4   OZRViewer                           0x000000010987e1cc -[OZCommandListenerObject processMessage:] + 244
5   Foundation                          0x000000018360f3d4 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10400724
6   Foundation                          0x000000018360f570 309E2D0A-EEDB-312D-BBB9-BFDDAC76DA4A + 10401136
7   OZRViewer                           0x0000000109ac29d4 _Z11SendMessagePvjyx + 220
8   OZRViewer                           0x00000001097de184 _ZN16CNotifierToEvent8OZNotifyE7CStringR10OZAtlArrayIS0_15OZElementTraitsIS0_EEbbi + 520
9   OZRViewer                           0x0000000108f71614 _ZN6OZCOne28CallOZEFormInputEventCommandE7CStringi + 732
10  OZRViewer                           0x0000000108f83bd8 _ZN8OZCOneIC11OnKillFocusEib + 244
11  OZRViewer                           0x0000000109de2568 _ZN16OZInputComponent11OnKillFocusEv + 144
12  OZRViewer                           0x0000000109bf0904 -[XSignButton onKillFocus] + 300
13  OZRViewer                           0x0000000109bed06c -[XSignButton closeUI:] + 1524
14  OZRViewer                           0x0000000109bed418 -[XSignButton closeDialogUI:] + 112
15  OZRViewer                           0x0000000109bed530 -[XSignButton resignFirstResponder] + 248
16  OZRViewer                           0x0000000109a1e5d4 -[XReportView resignFirstResponderForSubviews:docIndex:pageIndex:] + 1556
17  OZRViewer                           0x0000000109a1ed74 -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 1168
18  OZRViewer                           0x0000000109877fe0 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
19  OZRViewer                           0x00000001095ce76c _ZN18OZCViewerReportDoc15OnCheckValidityEP7OZCPage + 212
20  OZRViewer                           0x00000001099c3950 _ZN12OZCMainFrame14GetInformationE7CString + 22228
21  OZRViewer                           0x0000000109a9e5cc -[OZReportViewerImpl GetInformation:] + 424
22  FPPlanner_QA.debug.dylib            0x00000001039e65a8 $s12FPPlanner_QA25SSPESubSignViewControllerC14getInformation33_04CE6BF62F5C95923C0232BF88D9C865LL6action05wkWebE0yAA0cD6ActionV_So05WKWebE0CSgtF + 976
23  FPPlanner_QA.debug.dylib            0x00000001039e4c00 $s12FPPlanner_QA25SSPESubSignViewControllerC17handleMessageBody33_04CE6BF62F5C95923C0232BF88D9C865LL_05wkWebE0ySDyAA0chI3KeyOypG_So05WKWebE0CSgtF + 648
24  FPPlanner_QA.debug.dylib            0x00000001039e43a0 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtF + 2116
25  FPPlanner_QA.debug.dylib            0x00000001039e5318 $s12FPPlanner_QA25SSPESubSignViewControllerC011userContentF0_10didReceiveySo06WKUserhF0C_So15WKScriptMessageCtFTo + 68
26  WebKit                              0x00000001a0d13674 9B408D7C-337B-3328-8A80-C331F371C59D + 7464564
27  WebKit                              0x00000001a13c2dd8 9B408D7C-337B-3328-8A80-C331F371C59D + 14474712
28  WebKit                              0x00000001a12f5370 9B408D7C-337B-3328-8A80-C331F371C59D + 13632368
29  WebKit                              0x00000001a068a330 9B408D7C-337B-3328-8A80-C331F371C59D + 611120
30  WebKit                              0x00000001a0678234 9B408D7C-337B-3328-8A80-C331F371C59D + 537140
31  WebKit                              0x00000001a0687e18 9B408D7C-337B-3328-8A80-C331F371C59D + 601624
32  JavaScriptCore                      0x000000019b22988c D72A92C4-12ED-3239-9568-8950D3DE8B76 + 1575052
33  JavaScriptCore                      0x000000019b229644 D72A92C4-12ED-3239-9568-8950D3DE8B76 + 1574468
34  CoreFoundation                      0x0000000185650f10 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429840
35  CoreFoundation                      0x0000000185650e84 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 429700
36  CoreFoundation                      0x000000018562eb30 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 289584
37  CoreFoundation                      0x00000001856056d8 B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 120536
38  CoreFoundation                      0x0000000185604a6c B437A142-4F11-3EFF-B5AD-42A0F9BE9911 + 117356
39  GraphicsServices                    0x0000000227f6a498 GSEventRunModal + 120
40  UIKitCore                           0x000000018b0af70c 48736F98-163C-3430-AC20-54E325234380 + 648972
41  UIKitCore                           0x000000018b057f6c UIApplicationMain + 336
42  FPPlanner_QA.debug.dylib            0x00000001039515cc __debug_main_executable_dylib_entry_point + 184
43  dyld                                0x00000001825e2e28 1713978E-5F4F-366D-A258-5C6619465E97 + 20008





[DEBUG_CALLSTACK | Close Sign-2026-02-10 09:14:14.724 | <XSignButton: 0x14b982c00; frame = (216 3295.22; 82.205 18.1421); userInteractionEnabled = NO; backgroundColor = UIExtendedGrayColorSpace 0 0; layer = <CALayer: 0x10bd9b630>>] 호출 시점 로그: 
0   OZRViewer                           0x0000000109becb3c -[XSignButton closeUI:] + 196
1   OZRViewer                           0x0000000109bed418 -[XSignButton closeDialogUI:] + 112
2   OZRViewer                           0x0000000109bed530 -[XSignButton resignFirstResponder] + 248
3   OZRViewer                           0x0000000109a1e5d4 -[XReportView resignFirstResponderForSubviews:docIndex:pageIndex:] + 1556
4   OZRViewer                           0x0000000109a1ed74 -[XReportView flushInputControlsAtDocIndex:pageIndex:] + 1168
5   OZRViewer                           0x0000000109877fe0 _ZN19OZCViewerReportView28flushInputControlsAtDocIndexEii + 48
6   OZRViewer                           0x00000001095ce76c _ZN18OZCViewerReportDoc15OnCheckValidityEP7OZCPa
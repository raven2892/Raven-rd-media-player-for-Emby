# Raven rd media player for Emby

[简体中文](README.md) | [English](README_EN.md)

Raven rd media player for Emby is a native third-party Emby client and media player for Windows. Its interface is built with WPF and playback is powered by the bundled libmpv engine. It does not rely on WebView, Electron, or an external player window.

## About

Raven rd media player for Emby started from a very simple need: I had never found an Emby client on Windows that truly matched the way I wanted to use it while also providing a playback experience I was satisfied with, so I eventually decided to design and develop one myself.

The playback experience of Raven rd has always been centered around HDR, with Dolby Vision Profile 8.1 and Profile 5 being among the main areas of optimization. After many rounds of adjustment and testing with real-world media, the current dynamic brightness mapping is able to provide highlight control, shadow detail, and overall image depth that, subjectively, comes very close to the experience I get when playing Dolby Vision content on Apple devices.

From interface design and playback features to compatibility testing, Raven rd has always been developed independently by me. The project has gone through many versions, rewrites, tests, and abandoned early approaches. After continuous refinement, it has now largely reached a stable form and is suitable for everyday use.

Raven rd originally began as a personal project and a way for me to learn, while also hopefully giving other Windows Emby users another option.

Because the project is independently developed, tested, and maintained by one person, the amount of time and effort I can dedicate to it is limited. Bug testing, hardware compatibility, media format coverage, and issue resolution therefore cannot cover every possible scenario, and updates may not always be released promptly. Future development will depend on actual usage, user feedback, and the time I have available. There is currently no fixed release schedule.

I was previously a Jellyfin user as well, but due to the relatively long stable-release cycle and various issues I encountered during everyday use, I later switched to Emby. Jellyfin support may be added in the future, but whether and when that happens will depend on actual demand and user feedback.

The goal of Raven rd is to bring Emby media library management, remote playback, local media playback, and native Windows audio/video capabilities together in one unified desktop application.

Unlike clients that are essentially web applications wrapped inside a desktop shell, directly uses native Windows windows, D3D11 video output, WASAPI audio, and Windows display device information. This allows it to handle HDR, audio output, subtitles, playback controls, and local media files more directly.

> **Raven rd is independently developed, tested, and maintained by one person, and will always be provided free of charge.**

**Bilibili:** [Raven rd](https://space.bilibili.com/254066491)
Feature showcases, usage demonstrations, and future update information will gradually be published on Bilibili.

## Intended Use and STRM Support Statement

Raven rd is software developed around my own personal needs and shared with others free of charge. It is primarily designed around my own Emby and NAS environment. Feature priorities and maintenance decisions are based on my actual usage requirements and the amount of time I can personally dedicate to the project. It is not intended to support every possible use case.

**Raven rd does not support directly opening or parsing `.strm` files, and there are currently no plans to add this feature.** My media files are stored on my own NAS, and I do not use STRM-based media libraries or have a suitable STRM testing environment. As a result, STRM-based playback workflows are outside the scope of Raven rd's compatibility testing and dedicated support.

The fact that Emby itself supports STRM does not mean that Raven rd guarantees compatibility with every STRM-based playback workflow.

If STRM support is essential to your setup, please use another player that explicitly supports it.

Constructive and specific feedback is welcome, and I will respond or make improvements where my ability and available time allow. Baseless accusations, personal attacks, or intentionally provocative communication will not receive a response.

## Main Features

### Interface Preview

<table>
  <tr>
    <td><a href="assets/CN01.png"><img src="assets/EN01.png" width="100%"></a></td>
    <td><a href="assets/CN02.png"><img src="assets/EN02.png" width="100%"></a></td>
    <td><a href="assets/CN03.png"><img src="assets/EN03.png" width="100%"></a></td>
  </tr>
  <tr>
    <td><a href="assets/CN04.png"><img src="assets/EN04.png" width="100%"></a></td>
    <td><a href="assets/CN05.png"><img src="assets/EN05.png" width="100%"></a></td>
    <td></td>
  </tr>
</table>

### Emby Client

* Connect to an Emby server and sign in with a user account.
* Stores session access tokens without storing user passwords.
* Browse media libraries, recently added content, Continue Watching, and media details.
* Supports movies, TV series, seasons, episodes, collections, and people information.
* Supports media library search, sorting, filtering, and waterfall-style card layouts.
* Supports Emby playback URLs, subtitle URLs, audio track information, and playback progress synchronization.

### Native Playback

* Powered by the bundled libmpv playback engine.
* Uses a native Win32 video window with D3D11 output.
* Supports playback statistics, media information, audio channel levels, and real-time playback status.
* Supports Skip Intro controls.
* Supports Picture-in-Picture playback with a separate PiP control window.
* Supports multiple audio tracks, external subtitles, subtitle selection, and subtitle delay adjustment.
* Supports subtitle font, size, color, opacity, shadow, outline, position, and other styling options.
* Supports exporting currently downloadable text subtitles to local storage while applying the current subtitle delay.

### Local Playback

* Can be registered as the default Windows video player and opened directly through Windows file associations without requiring an Emby login.
* Supports selecting multiple local files and creating a temporary playback queue for the current session.
* Local playback uses the same native playback interface, controls, subtitle settings, and audio settings as Emby playback.

### HDR, SDR, and Video Enhancement

* Reads Windows HDR status, DXGI color space, graphics adapter information, and display device information for the monitor containing the current playback window.
* Supports native HDR output and selects the appropriate D3D11/libplacebo output path according to the capabilities of the current display.
* When Windows HDR is disabled, HDR-to-SDR tone mapping is available to preserve highlights, contrast, and color depth as much as possible.
* Supports HDR10 and HLG, and provides identification and dedicated playback paths for certain Dolby Vision profiles.
* Provides dedicated playback optimizations, including dynamic brightness mapping, for Dolby Vision Profile 8.1 and Profile 5 content.
* Provides basic playback diagnostic information such as HDR peak brightness, output color space, and display status.
* Supports invoking NVIDIA RTX HDR for eligible non-native-HDR content.
* Supports invoking NVIDIA RTX Video Super Resolution (RTX VSR) for eligible video enhancement.

Video enhancement features depend on hardware and drivers. Whether they can actually be enabled depends on the GPU, driver version, display, Windows HDR state, media type, and current video output path.

### Audio and Spatial Audio

* Supports standard WASAPI audio output.
* Supports Windows Spatial Audio status detection and related playback paths.
* Supports multichannel audio, audio track selection, and independent channel volume adjustment.
* Supports real-time audio level monitoring, including RMS and peak levels for decoded PCM channels.
* Supports conventional decoding and multichannel playback of formats including Dolby Digital Plus and TrueHD.
* For certain media containing object-based audio metadata, Raven can extract available object information and map it within its own playback pipeline to an output path of up to 12 channels, with the goal of preserving as much spatial information from the original sound field as possible.
* This processing method is Raven's own multichannel spatial-audio implementation. It is **not** an official Dolby Atmos decoder, passthrough implementation, or Dolby-certified solution.
* Actual output depends on the source media, decoding path, Windows Spatial Audio, default playback device, drivers, and final audio hardware.

### Interface and Personalization

* Unified dark native desktop interface.
* The home page, media library, detail pages, playback controls, and settings use a consistent visual language and material system.
* Supports default backgrounds, custom backgrounds, background opacity adjustment, accent colors, and multiple interface materials.
* Supports immersive backgrounds, waterfall-style layouts, pill-shaped navigation, and search access.
* Supports switching between Chinese and English interfaces.

## System Requirements

### Basic Requirements

* Windows 10 version 2004 (Build 19041) or later.
* 64-bit Windows.
* x64 processor.
* Graphics driver with Direct3D 11 support.
* Emby features require access to a valid Emby server with appropriate user permissions.

The installer is provided for Windows x64. Required .NET runtime components are included with the release package, but the system must still be capable of running WPF, D3D11, Windows Core Audio, and the relevant Windows graphics interfaces correctly.

### HDR and Video Enhancement Requirements

* Native HDR requires an HDR-capable display, Windows HDR, and a GPU/driver capable of HDR output.
* HDR-to-SDR conversion can be used on SDR displays, but final image quality depends on the media source, display brightness, color gamut, and user settings.
* RTX HDR and RTX VSR require a supported NVIDIA GPU, compatible drivers, and media that meets the corresponding requirements.
* 4K, high-bitrate, HDR, Dolby Vision, and multichannel media may increase GPU, CPU, VRAM, storage, and network bandwidth requirements.

### Spatial Audio Requirements

* Spatial audio features depend on Windows audio settings, the current default playback device, drivers, and output hardware.
* Actual playback capability for Dolby Digital Plus, TrueHD, and other multichannel audio formats depends on the source media, decoding path, and system audio environment.
* For certain media containing object-based audio information, Raven may perform multichannel mapping based on available object metadata, using an output path of up to 12 channels.
* Object-audio processing is not an official Dolby Atmos decoder or certified implementation. Final spatial imaging and soundstage performance depend on Windows Spatial Audio, playback hardware, and system configuration.

## Usage

### Connecting to Emby

1. Launch Raven rd.
2. Enter the root address of your Emby server, for example `https://example.com` or `https://example.com/emby`.
3. Enter your Emby username and password and sign in.
4. After signing in successfully, select content from the Home page or the media library navigation on the left.
5. Select a movie, series, or episode to open its detail page and begin playback.

### Playing Local Videos

1. Select **Open Local Video** on the login page.
2. Select one or more local video files.
3. The selected files will be added to a playback queue for the current session.
4. You can use Previous, Next, Playlist, Subtitles, Audio Track, and other playback controls.

Local playback does not require an Emby connection and will not synchronize playback progress with the Emby Continue Watching list.

### Adjusting Subtitles

Subtitle settings allow you to adjust font, size, color, opacity, shadow, outline, position, and delay.

Subtitle settings apply to both local playback and Emby media.

## Issue Reporting

If you encounter an issue, you can submit a report through GitHub Issues. When reporting a problem, please provide as much of the following information as possible:

* Windows version and system update/build.
* GPU model and driver version.
* Whether Windows HDR is enabled on the display.
* Emby server version, connection method, and media type.
* Whether the issue occurs during Emby playback or local playback.
* Whether the issue involves HDR, Dolby Vision, RTX HDR, RTX VSR, spatial audio, or subtitles.
* Reproduction steps, error messages, and relevant screenshots where necessary.

> **Do not post your Emby password, access token, private server address, or other personal or sensitive information in a public GitHub Issue.**

## Support Raven rd

<p align="center">
  <a href="assets/02.png">
    <img src="assets/01.png" width="100%">
  </a>
</p>

## Third-Party Components

Raven rd uses or integrates the following third-party components, system technologies, development tools, and external interfaces:

* .NET 8 and WPF.
* libmpv and its FFmpeg decoding, filtering, and playback capabilities.
* libplacebo for video color management, HDR processing, and tone mapping.
* D3D11, DXGI, Windows Core Audio, WASAPI, and Windows Spatial Audio.
* Microsoft Windows App SDK, Win2D, and InteropCompositor-related components.
* Fluent System Icons font resources.
* WiX Toolset 4 for building the Windows installer.
* Emby REST API for server authentication, media libraries, media details, playback URLs, subtitles, and playback progress synchronization.

Third-party components used by Raven rd remain the property of their respective authors or rights holders and are used in accordance with their applicable licenses.

Third-party components distributed with Raven rd will retain the copyright notices and license information required by their respective licenses.

Raven rd does not include Emby Server and does not provide or modify the Emby server software.

## Disclaimer

* Raven rd is an independently developed third-party Windows client. It is not affiliated with, endorsed by, or certified by Emby.
* Raven rd is intended only for accessing Emby servers and media content that the user is authorized to access.
* Playback capabilities and final playback quality may be affected by media containers, codecs, server configuration, network conditions, GPU hardware, drivers, display devices, audio devices, and Windows system settings.
* Availability and functionality of HDR, Dolby Vision, RTX HDR, RTX VSR, spatial audio, and related features depend on the corresponding hardware, operating system, drivers, and underlying technologies.
* Users are responsible for ensuring that their use of servers, media files, subtitles, and playback devices complies with applicable local laws, regulations, licensing requirements, and content or service authorization terms.
* The software is provided free of charge and on an "as is" basis. To the extent permitted by applicable law, the developer shall not be liable for playback interruptions, data loss, hardware or software compatibility issues, or other indirect losses resulting from the use of Raven.

## Copyright

* Copyright © 2026 Raven rd. All rights reserved.
* Except for content explicitly identified as third-party material, the rights to Raven's original program code, interface design, documentation, configuration files, scripts, and other original content belong to Raven rd.
* Raven may be downloaded, installed, and used for personal purposes free of charge. Without authorization, Raven may not be repackaged, redistributed, presented as an official version, or used together with the Raven rd name, branding, interface assets, or other original content to create misleading derivative versions.
* Third-party components, fonts, icons, trademarks, and other third-party content remain the property of their respective authors or rights holders and are used in accordance with their applicable licenses or terms of use.

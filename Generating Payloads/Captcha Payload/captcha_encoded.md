
```py
def generate_random_fingerprint():
    cpu_cores_options = [2, 4, 6, 8, 12, 16]
    cpu_load = random.randint(1, 100)
    device_memory_gb = random.choice([4, 6, 8, 12, 16, 32])
    platforms = ['Win32', 'MacIntel', 'Linux x86_64', 'Android', 'iPhone']
    gpu_vendors = ['Intel', 'NVIDIA', 'AMD', 'Google Inc. (Intel)', 'Apple']
    gpu_renderers = [
        "ANGLE (Intel, Intel(R) UHD Graphics 630 Direct3D11 vs_5_0 ps_5_0)",
        "ANGLE (NVIDIA GeForce GTX 1060 Direct3D11 vs_5_0 ps_5_0)",
        "ANGLE (AMD Radeon RX 580 Direct3D11 vs_5_0 ps_5_0)",
        "Apple A13 GPU",
        "Google SwiftShader"
    ]
    battery_charging = random.choice([True, False])
    battery_level = round(random.uniform(0, 1), 2)
    stylus_detection = random.choice(['Yes', 'No'])
    touch_support = random.choice(['Yes', 'No'])
    timezone = random.choice(['Africa/Cairo', 'America/New_York', 'Europe/London', 'Asia/Tokyo'])
    languages = ['en-US', 'fr-FR', 'es-ES', 'de-DE', 'zh-CN']
    user_agents = [
        "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36",
        "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15",
        "Mozilla/5.0 (Linux; Android 10; SM-G973F) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Mobile Safari/537.36",
        "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1"
    ]
    screen_widths = [1280, 1366, 1440, 1536, 1600, 1920, 2560]
    screen_heights = [720, 768, 900, 1024, 1080, 1440, 1600]
    color_depth = random.choice([24, 30, 32])
    device_pixel_ratio = random.choice([1, 1.25, 1.5, 2, 3])

    fingerprint = {
        "deviceInfo": {
            "cpuCores": random.choice(cpu_cores_options),
            "cpuLoad": cpu_load,
            "deviceMemoryGB": device_memory_gb,
            "platform": random.choice(platforms),
            "maxTouchPoints": 0 if touch_support == 'No' else random.choice([1, 5, 10]),
            "msMaxTouchPoints": 'Not Supported',
            "gpu": {
                "vendor": random.choice(gpu_vendors),
                "renderer": random.choice(gpu_renderers)
            },
            "battery": {
                "charging": battery_charging,
                "level": battery_level,
                "chargingTime": 0 if battery_charging else random.randint(1000, 5000),
                "dischargingTime": None if battery_charging else random.randint(10000, 20000)
            },
            "stylusDetection": stylus_detection,
            "touchSupport": touch_support
        },
        "browserInfo": {
            "userAgent": random.choice(user_agents),
            "timezone": timezone,
            "timezoneOffset": -180 if timezone == 'Africa/Cairo' else random.choice([-300, 0, 540]),
            "localeDateTime": time.strftime("%m/%d/%Y, %I:%M:%S %p"),
            "localUnixTime": int(time.time()),
            "calendar": "gregory",
            "day": "numeric",
            "locale": "en-US",
            "month": "numeric",
            "numberingSystem": "latn",
            "year": "numeric",
            "appName": "Netscape",
            "appVersion": "5.0 (Windows NT 10.0; Win64; x64)",
            "vendor": "Google Inc.",
            "language": random.choice(languages),
            "languages": languages,
            "cookieEnabled": True,
            "onlineStatus": "Online",
            "javaEnabled": False,
            "doNotTrack": None,
            "referrerHeader": "https://www.google.com/",
            "httpsConnection": "Yes",
            "historyLength": random.randint(1, 10),
            "mimeTypes": random.randint(5, 20),
            "plugins": random.randint(1, 10),
            "webdriver": False,
            "pageVisibility": "visible",
            "isBot": "No",
            "featuresSupported": {
                "geolocation": "Yes",
                "serviceWorker": "Yes",
                "localStorage": "Yes",
                "sessionStorage": "Yes",
                "indexedDB": "Yes",
                "notifications": "Yes",
                "notificationsFirebase": "default",
                "clipboard": "Yes",
                "pushAPI": "Yes",
                "webRTC": "Yes",
                "gamepadAPI": "Yes",
                "speechSynthesis": "Yes",
                "webGL": "Yes",
                "vibrationAPI": "Yes",
                "deviceMotion": "Yes",
                "deviceOrientation": "Yes",
                "wakeLock": "Yes",
                "serial": "Yes",
                "usb": "Yes",
                "networkInformation": "Yes",
                "screenCapture": "Yes",
                "fullscreenAPI": "Yes",
                "pictureInPicture": "Yes"
            }
        },
        "screenInfo": {
            "width": random.choice(screen_widths),
            "height": random.choice(screen_heights),
            "colorDepth": color_depth,
            "pixelDepth": color_depth,
            "devicePixelRatio": device_pixel_ratio,
            "orientation": "landscape-primary",
            "screenOrientationAngle": 0,
            "availableWidth": random.choice(screen_widths),
            "availableHeight": random.choice(screen_heights),
            "screenLeft": 0,
            "screenTop": 0,
            "outerWidth": random.choice(screen_widths),
            "outerHeight": random.choice(screen_heights),
            "innerWidth": random.choice(screen_widths),
            "innerHeight": random.choice(screen_heights)
        },
        "otherData": {
            "mouseAvailable": "Yes",
            "keyboardAvailable": "Yes",
            "bluetoothSupport": "Yes",
            "usb exacerbate": "Yes",
            "gamepadSupport": "Yes",
            "incognitoMode": False
        },
        "storageInfo": {
            "localStorage": 1,
            "sessionStorage": 1,
            "indexedDB": "Available",
            "cacheStorage": "Available",
            "storageEstimate": {
                "quota": random.randint(500000000, 2000000000),
                "usage": random.randint(1000000, 100000000),
                "usageDetails": {}
            }
        }
    }

    return json.dumps(fingerprint, indent=2)
```

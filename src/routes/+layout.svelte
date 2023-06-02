<script lang="ts">
    import * as THREE from 'three'

	enum Theme {
		Dark,
		Light
	}
    interface Color {
        r: number;
        g: number;
        b: number;
    }
	interface ThemeProperties {
		bgGradientDark: Color;
		bgGradientLight: Color;
        text: Color;
	}

	class ThemeData {
        readonly theme: Theme;
		properties: ThemeProperties;

		constructor(theme: Theme, properties: ThemeProperties) {
            this.theme = theme;
			this.properties = properties;
		}

		exportToCssText(): string {
			let values: Array<string> = [];
			values.push(`--theme-bg-gradient-dark:rgb(${Math.round(this.properties.bgGradientDark.r)}, ${Math.round(this.properties.bgGradientDark.g)}, ${Math.round(this.properties.bgGradientDark.b)})`);
			values.push(`--theme-bg-gradient-light:rgb(${Math.round(this.properties.bgGradientLight.r)}, ${Math.round(this.properties.bgGradientLight.g)}, ${Math.round(this.properties.bgGradientLight.b)})`);
            values.push(`--theme-text:rgb(${Math.round(this.properties.text.r)}, ${Math.round(this.properties.text.g)}, ${Math.round(this.properties.text.b)})`);
			return values.join(';');
		}
	}

    let interpolated = false;
	let theme: Theme = Theme.Dark;
    let targetTheme: ThemeData;
	const darkTheme: ThemeData = new ThemeData(Theme.Dark, {
		bgGradientDark: {r: 27, g: 32, b: 51},
		bgGradientLight: {r: 38, g: 45, b: 51},
        text: {r: 255, b: 255, g: 255}
	});
	const lightTheme: ThemeData = new ThemeData(Theme.Light, {
		bgGradientDark: {r: 194, g: 194, b: 194},
		bgGradientLight: {r: 232, g: 232, b: 232},
        text: {r: 10, b: 10, g: 10}
	});
    const currentTheme: ThemeData = new ThemeData(theme, {
        bgGradientDark: darkTheme.properties.bgGradientDark,
        bgGradientLight: darkTheme.properties.bgGradientLight,
        text: darkTheme.properties.text
    });

	const toggleTheme = () => {
		if (theme == Theme.Dark) {
			theme = Theme.Light;
		} else {
			theme = Theme.Dark;
		}
		setTheme(theme);
	};
	const setTheme = (theme: Theme) => {
		switch (theme) {
			case Theme.Dark:
				targetTheme = darkTheme;
				break;
			case Theme.Light:
				targetTheme = lightTheme;
				break;
		}
		
        if (!interpolated) {
            interpolate();
            interpolated = true;
        }
	};
    const interpolate = () => {
        currentTheme.properties = {
            bgGradientDark: {
                r: THREE.MathUtils.lerp(currentTheme.properties.bgGradientDark.r, targetTheme.properties.bgGradientDark.r, 0.1),
                g: THREE.MathUtils.lerp(currentTheme.properties.bgGradientDark.g, targetTheme.properties.bgGradientDark.g, 0.1),
                b: THREE.MathUtils.lerp(currentTheme.properties.bgGradientDark.b, targetTheme.properties.bgGradientDark.b, 0.1),
            },
            bgGradientLight: {
                r: THREE.MathUtils.lerp(currentTheme.properties.bgGradientLight.r, targetTheme.properties.bgGradientLight.r, 0.1),
                g: THREE.MathUtils.lerp(currentTheme.properties.bgGradientLight.g, targetTheme.properties.bgGradientLight.g, 0.1),
                b: THREE.MathUtils.lerp(currentTheme.properties.bgGradientLight.b, targetTheme.properties.bgGradientLight.b, 0.1),
            },
            text: {
                r: THREE.MathUtils.lerp(currentTheme.properties.text.r, targetTheme.properties.text.r, 0.1),
                g: THREE.MathUtils.lerp(currentTheme.properties.text.g, targetTheme.properties.text.g, 0.1),
                b: THREE.MathUtils.lerp(currentTheme.properties.text.b, targetTheme.properties.text.b, 0.1),
            }
        }

        document.documentElement.style.cssText = currentTheme.exportToCssText();

        requestAnimationFrame(interpolate);
    }
</script>

<main>
    <button on:click={toggleTheme}>Toggle</button>

	<slot />
</main>

<style>
    :root {
        --theme-bg-gradient-dark: rgb(27, 32, 51);
        --theme-bg-gradient-light: rgb(38, 45, 51);
        --theme-text: rgb(255, 255, 255);
    }

	main {
        min-height: 100vh;
		background: var(--theme-bg-gradient-dark);
		background: -moz-radial-gradient(
			circle,
			var(--theme-bg-gradient-light) 0%,
			var(--theme-bg-gradient-dark) 100%
		);
		background: -webkit-radial-gradient(
			circle,
			var(--theme-bg-gradient-light) 0%,
			var(--theme-bg-gradient-dark) 100%
		);
		background: radial-gradient(
			circle,
			var(--theme-bg-gradient-light) 0%,
			var(--theme-bg-gradient-dark) 100%
		);
	}
</style>

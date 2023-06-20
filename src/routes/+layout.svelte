<script lang="ts">
    import * as THREE from 'three';
    import { Theme } from '../stores/theme';
    import StaticNavigationBar from '../components/StaticNavigationBar.svelte';

    interface Color {
        r: number;
        g: number;
        b: number;
    }
    interface ThemeProperties {
        bgGradientDark: Color;
        bgGradientLight: Color;
        textBase: Color;
        textShade: Color;
        textDescription: Color;
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
            values.push(
                `--theme-bg-gradient-dark:rgb(${Math.round(
                    this.properties.bgGradientDark.r
                )}, ${Math.round(this.properties.bgGradientDark.g)}, ${Math.round(
                    this.properties.bgGradientDark.b
                )})`
            );
            values.push(
                `--theme-bg-gradient-light:rgb(${Math.round(
                    this.properties.bgGradientLight.r
                )}, ${Math.round(this.properties.bgGradientLight.g)}, ${Math.round(
                    this.properties.bgGradientLight.b
                )})`
            );
            values.push(
                `--theme-text-base:rgb(${Math.round(this.properties.textBase.r)}, ${Math.round(
                    this.properties.textBase.g
                )}, ${Math.round(this.properties.textBase.b)})`
            );
            values.push(
                `--theme-text-shade:rgb(${Math.round(this.properties.textShade.r)}, ${Math.round(
                    this.properties.textShade.g
                )}, ${Math.round(this.properties.textShade.b)})`
            );
            values.push(
                `--theme-text-description:rgb(${Math.round(
                    this.properties.textDescription.r
                )}, ${Math.round(this.properties.textDescription.g)}, ${Math.round(
                    this.properties.textDescription.b
                )})`
            );
            return values.join(';');
        }
    }

    let interpolated = false;
    let theme: Theme = Theme.Dark;
    let previousTheme: Theme = theme;
    let targetTheme: ThemeData;
    const darkTheme: ThemeData = new ThemeData(Theme.Dark, {
        bgGradientDark: { r: 27, g: 32, b: 51 },
        bgGradientLight: { r: 38, g: 45, b: 71 },
        textBase: { r: 237, b: 237, g: 237 },
        textShade: { r: 130, b: 130, g: 130 },
        textDescription: { r: 183, g: 183, b: 183 }
    });
    const lightTheme: ThemeData = new ThemeData(Theme.Light, {
        bgGradientDark: { r: 194, g: 194, b: 194 },
        bgGradientLight: { r: 232, g: 232, b: 232 },
        textBase: { r: 10, b: 10, g: 10 },
        textShade: { r: 100, b: 100, g: 100 },
        textDescription: { r: 40, g: 40, b: 40 }
    });
    const lowVisionTheme: ThemeData = new ThemeData(Theme.LowVision, {
        bgGradientDark: {r: 0, g: 0, b: 0},
        bgGradientLight: {r: 0, g: 0, b: 0},
        textBase: { r: 255, g: 253, b: 72 },
        textShade: { r: 255, g: 253, b: 72 },
        textDescription: { r: 255, g: 253, b: 72 }
    });
    const currentTheme: ThemeData = new ThemeData(theme, {
        bgGradientDark: darkTheme.properties.bgGradientDark,
        bgGradientLight: darkTheme.properties.bgGradientLight,
        textBase: darkTheme.properties.textBase,
        textShade: darkTheme.properties.textShade,
        textDescription: darkTheme.properties.textDescription
    });

    const toggleTheme = () => {
        if (theme == Theme.LowVision) {
            return;
        }
        if (theme == Theme.Dark) {
            theme = Theme.Light;
        } else {
            theme = Theme.Dark;
        }
        setTheme(theme);
    };
    const toggleLowVision = () => {
        if (theme == Theme.LowVision) {
            theme = previousTheme;
        } else {
            previousTheme = theme;
            theme = Theme.LowVision;
        }
        setTheme(theme);
    }

    const setTheme = (theme: Theme) => {
        switch (theme) {
            case Theme.Dark:
                targetTheme = darkTheme;
                break;
            case Theme.Light:
                targetTheme = lightTheme;
                break;
            case Theme.LowVision:
                targetTheme = lowVisionTheme;
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
                r: THREE.MathUtils.lerp(
                    currentTheme.properties.bgGradientDark.r,
                    targetTheme.properties.bgGradientDark.r,
                    0.1
                ),
                g: THREE.MathUtils.lerp(
                    currentTheme.properties.bgGradientDark.g,
                    targetTheme.properties.bgGradientDark.g,
                    0.1
                ),
                b: THREE.MathUtils.lerp(
                    currentTheme.properties.bgGradientDark.b,
                    targetTheme.properties.bgGradientDark.b,
                    0.1
                )
            },
            bgGradientLight: {
                r: THREE.MathUtils.lerp(
                    currentTheme.properties.bgGradientLight.r,
                    targetTheme.properties.bgGradientLight.r,
                    0.1
                ),
                g: THREE.MathUtils.lerp(
                    currentTheme.properties.bgGradientLight.g,
                    targetTheme.properties.bgGradientLight.g,
                    0.1
                ),
                b: THREE.MathUtils.lerp(
                    currentTheme.properties.bgGradientLight.b,
                    targetTheme.properties.bgGradientLight.b,
                    0.1
                )
            },
            textBase: {
                r: THREE.MathUtils.lerp(
                    currentTheme.properties.textBase.r,
                    targetTheme.properties.textBase.r,
                    0.1
                ),
                g: THREE.MathUtils.lerp(
                    currentTheme.properties.textBase.g,
                    targetTheme.properties.textBase.g,
                    0.1
                ),
                b: THREE.MathUtils.lerp(
                    currentTheme.properties.textBase.b,
                    targetTheme.properties.textBase.b,
                    0.1
                )
            },
            textShade: {
                r: THREE.MathUtils.lerp(
                    currentTheme.properties.textShade.r,
                    targetTheme.properties.textShade.r,
                    0.1
                ),
                g: THREE.MathUtils.lerp(
                    currentTheme.properties.textShade.g,
                    targetTheme.properties.textShade.g,
                    0.1
                ),
                b: THREE.MathUtils.lerp(
                    currentTheme.properties.textShade.b,
                    targetTheme.properties.textShade.b,
                    0.1
                )
            },
            textDescription: {
                r: THREE.MathUtils.lerp(
                    currentTheme.properties.textDescription.r,
                    targetTheme.properties.textDescription.r,
                    0.1
                ),
                g: THREE.MathUtils.lerp(
                    currentTheme.properties.textDescription.g,
                    targetTheme.properties.textDescription.g,
                    0.1
                ),
                b: THREE.MathUtils.lerp(
                    currentTheme.properties.textDescription.b,
                    targetTheme.properties.textDescription.b,
                    0.1
                )
            }
        };

        document.documentElement.style.cssText = currentTheme.exportToCssText();

        requestAnimationFrame(interpolate);
    };
</script>

<main>
    <StaticNavigationBar {theme} on:toggleTheme={toggleTheme} on:toggleLowVision={toggleLowVision}/>
    <slot />
</main>

<style>
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

    main :global(h1) {
        color: transparent;
        background: var(--theme-text-base);
        background: linear-gradient(
            138deg,
            var(--theme-text-base) 75%,
            var(--theme-text-shade) 100%
        );
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }
</style>

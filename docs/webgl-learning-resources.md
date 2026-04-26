# webgl learning resources

## core references

**webgl api reference** — [mdn webgl rendering context](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_Rendering_Context)
complete api reference for webgl methods, properties, browser compatibility

**glsl tutorial** — [iquanli glsl tutorial](https://iquanli.com/tutorial/glsl-tutorial/)
opengl shading language fundamentals: vertex + fragment shader programming, built-in functions

**webgl examples** — [webgl.org examples](https://examples.webgl.org/)
practical implementations, interactive demos, common pattern reference

## frameworks + libraries

**babylon.js** — [babylonjs.com](https://www.babylonjs.com/)
high-level webgl framework covering scene management, physics, particles, advanced effects

## mathematical foundations

**3blue1brown — linear algebra** — [youtube playlist](https://www.youtube.com/playlist?list=PLZHQObOWTQDlr1V0Y6xVImDUzMgkyHcdm)
visual linear algebra: matrix transformations, vector operations — essential math for 3d graphics

## scenes on bryanchasko.com

all scenes extend `BaseScene.js` with standardized lifecycle methods (`init`, `animate`, `destroy`)

| file                    | effect                      |
| ----------------------- | --------------------------- |
| `OrbitScene.js`         | particle orbit animations   |
| `TransitionScene.js`    | scene transition management |
| `RippleScene.js`        | water ripple effects        |
| `SkillsNetworkScene.js` | network graph visualization |
| `ShimmerScene.js`       | shimmer / glow pass         |

lives in `themes/bryan-chasko-theme/assets/js/webgl-scenes/`

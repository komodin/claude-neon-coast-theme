# Neon Coast: a theme for Claude

A neon tropical sunset for the Claude app, with a GTA VI vibe but with its own artwork. It comes with two things:

- **A complete palette** for light and dark mode: violet grays, magenta for actions, and cyan as a counterpoint in code.
- **An animated background** behind the conversation:
  - an Art Deco skyline with its reflection in the water and a lit causeway crossing the bay;
  - the striped sun;
  - swaying palm trees and gusts of wind that sweep from left to right.

  On mobile, the background has its own vertical composition.

Light mode is a peach and turquoise dawn with golden details. Dark mode is an indigo night with pink and cyan neon.

## Requirements

- **The Claude desktop app (or the mobile one), up to date.** The theme is drawn there. It does not show up in the terminal or in editors, because they don't draw themes.
- **A recent Claude Code.** The theme is a *mod*: a plugin with a hooks module that uses the Claude Code mods API. That API is in early access and may change between versions.
- **You don't need Node or anything else installed.** It's four text files.

## The easy way: ask Claude

Open a Claude Code session (in the desktop app or in the terminal), attach this file and write:

> Install the theme from this file: create the folder `~/claude-themes/neon-coast` with its files and activate it with method A.

Claude creates the files and runs the commands. Then open a new session and you're done.

## Manual installation

### 1. Create the folder and the files

Create this structure. The path is a suggestion: it can be any folder of yours.

```text
~/claude-themes/neon-coast/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
└── hooks/
    ├── hooks.json
    └── register.tsx
```

Copy each file exactly as it is. `register.tsx` is long because it draws the whole scene: copy it in full.

**`neon-coast/.claude-plugin/plugin.json`**

```json
{
  "description": "Neon Coast: a neon tropical sunset theme with an animated Art Deco skyline, palms and sea, in light and dark",
  "name": "neon-coast",
  "version": "1.0.0"
}
```

**`neon-coast/.claude-plugin/marketplace.json`**

```json
{
  "description": "Neon Coast, a theme for the Claude desktop and mobile apps",
  "name": "neon-coast",
  "owner": {
    "name": "Neon Coast"
  },
  "plugins": [
    {
      "description": "Neon tropical sunset theme for the Claude desktop and mobile apps",
      "name": "neon-coast",
      "source": "./"
    }
  ]
}
```

**`neon-coast/hooks/hooks.json`**

```json
{
  "modules": ["./register.tsx"]
}
```

**`neon-coast/hooks/register.tsx`**

```tsx
import type { Register, ThemeColors, ThemeSetArgs } from 'claude-code'

const SCENE_NAME = 'neon-coast'

// Hot dusk: magenta takes action, cyan answers it in code and on the water,
// warm sunset hues keep their meaning (red danger, amber warning, mint success).
// Precomputed from five role colors and six gray anchors per mode with the
// color helper of Claude Code's plugin-authoring skill, so this file needs nothing else.
const COLORS: ThemeColors = {
  id: 'mod-theme',
  inputs: {
    dark: {
      'fill-git-added': '#34e3a4',
      'fill-git-modified': '#ffb340',
      'gray-0': '#ffffff',
      'gray-10': '#fffefe',
      'gray-100': '#f5e3f1',
      'gray-150': '#ead5ea',
      'gray-20': '#fffbfc',
      'gray-200': '#e0c8e4',
      'gray-250': '#d7bfdc',
      'gray-30': '#fff8fa',
      'gray-300': '#cdb5d5',
      'gray-350': '#c4accd',
      'gray-40': '#fff4f8',
      'gray-400': '#bba3c6',
      'gray-450': '#a790b5',
      'gray-50': '#fff0f7',
      'gray-500': '#927ea4',
      'gray-550': '#7f6c94',
      'gray-60': '#fdedf6',
      'gray-600': '#6c5b83',
      'gray-650': '#5a4a73',
      'gray-70': '#fbebf5',
      'gray-700': '#483963',
      'gray-750': '#372954',
      'gray-80': '#f9e8f3',
      'gray-800': '#271944',
      'gray-810': '#251741',
      'gray-820': '#22163d',
      'gray-830': '#20143a',
      'gray-840': '#1d1236',
      'gray-850': '#190f2f',
      'gray-860': '#180e2d',
      'gray-870': '#160d2b',
      'gray-880': '#150c28',
      'gray-890': '#130b26',
      'gray-90': '#f7e5f2',
      'gray-900': '#120a24',
      'role-accent-100': '#ffd2de',
      'role-accent-250': '#ff86ac',
      'role-accent-300': '#ff669c',
      'role-accent-400': '#f30078',
      'role-accent-450': '#db006b',
      'role-accent-50': '#ffe9f0',
      'role-accent-600': '#960045',
      'role-accent-700': '#6a002e',
      'role-accent-800': '#42001c',
      'role-accent-850': '#2f0014',
      'role-accent-fill': '#db006b',
      'role-accent-fill-hover': '#f30078',
      'role-accent-on': '#ffffff',
      'role-danger-100': '#fdd5d2',
      'role-danger-250': '#f69289',
      'role-danger-300': '#f37a6e',
      'role-danger-400': '#eb3f27',
      'role-danger-450': '#d83016',
      'role-danger-600': '#931e0d',
      'role-danger-700': '#681408',
      'role-danger-800': '#3e0b06',
      'role-danger-fill': '#d83016',
      'role-danger-fill-hover': '#eb3f27',
      'role-danger-on': '#ffffff',
      'role-pro-100': '#a5edff',
      'role-pro-250': '#00c8e4',
      'role-pro-300': '#00b7d0',
      'role-pro-400': '#0098aa',
      'role-pro-450': '#008897',
      'role-pro-600': '#005c65',
      'role-pro-700': '#004046',
      'role-pro-800': '#00262a',
      'role-pro-fill': '#008897',
      'role-pro-fill-hover': '#0098aa',
      'role-pro-on': '#000000',
      'role-success-100': '#b0f1ce',
      'role-success-250': '#00d38d',
      'role-success-400': '#009f6a',
      'role-success-450': '#008f5e',
      'role-success-600': '#00603e',
      'role-success-700': '#00442a',
      'role-success-800': '#002817',
      'role-success-fill': '#008f5e',
      'role-success-fill-hover': '#009f6a',
      'role-success-on': '#120a24',
      'role-tooltip-bg': '#120a24',
      'role-tooltip-fg': '#ffffff',
      'role-warning-100': '#ffd9a6',
      'role-warning-200': '#ffae43',
      'role-warning-250': '#f9990b',
      'role-warning-300': '#e68c0c',
      'role-warning-600': '#784107',
      'role-warning-700': '#552b04',
      'role-warning-800': '#341801',
      'role-warning-fill': '#ffae43',
      'role-warning-fill-hover': '#f9990b',
      'role-warning-on': '#120a24',
      'text-git-added': '#34e3a4',
      'text-git-closed': '#ff7385',
      'text-git-conflicting': '#ff8a3d',
      'text-git-draft': '#b8abc6',
      'text-git-merged': '#c4a0ff',
      'text-git-modified': '#ffb340',
      'text-git-removed': '#ff5a6e',
    },
    light: {
      'fill-git-added': '#0a6442',
      'fill-git-modified': '#8b4f00',
      'gray-0': '#fdf5f0',
      'gray-10': '#faece4',
      'gray-100': '#d8c1c3',
      'gray-150': '#c5acb5',
      'gray-20': '#f7e4da',
      'gray-200': '#b397a7',
      'gray-250': '#a18399',
      'gray-30': '#f3e0d7',
      'gray-300': '#8e6e8b',
      'gray-350': '#7d5b7d',
      'gray-40': '#f0dcd4',
      'gray-400': '#6c4870',
      'gray-450': '#654068',
      'gray-50': '#ebd6d1',
      'gray-500': '#5d3961',
      'gray-550': '#563159',
      'gray-60': '#e7d2ce',
      'gray-600': '#4f2a52',
      'gray-650': '#49254c',
      'gray-70': '#e3cecb',
      'gray-700': '#432146',
      'gray-750': '#3d1c40',
      'gray-80': '#e0cac9',
      'gray-800': '#361839',
      'gray-810': '#351738',
      'gray-820': '#341637',
      'gray-830': '#331536',
      'gray-840': '#321435',
      'gray-850': '#311334',
      'gray-860': '#2f1233',
      'gray-870': '#2e1231',
      'gray-880': '#2d1130',
      'gray-890': '#2c102f',
      'gray-90': '#dcc5c6',
      'gray-900': '#2b0f2e',
      'role-accent-100': '#ffd2de',
      'role-accent-250': '#ff86ac',
      'role-accent-300': '#ff669c',
      'role-accent-400': '#f30078',
      'role-accent-450': '#db006b',
      'role-accent-50': '#ffe9f0',
      'role-accent-600': '#960045',
      'role-accent-700': '#6a002e',
      'role-accent-800': '#42001c',
      'role-accent-850': '#2f0014',
      'role-accent-fill': '#db006b',
      'role-accent-fill-hover': '#f30078',
      'role-accent-on': '#fdf5f0',
      'role-danger-100': '#fdd5d2',
      'role-danger-250': '#f69289',
      'role-danger-300': '#f37a6e',
      'role-danger-400': '#eb3f27',
      'role-danger-450': '#d83016',
      'role-danger-600': '#931e0d',
      'role-danger-700': '#681408',
      'role-danger-800': '#3e0b06',
      'role-danger-fill': '#d83016',
      'role-danger-fill-hover': '#eb3f27',
      'role-danger-on': '#ffffff',
      'role-pro-100': '#a5edff',
      'role-pro-250': '#00c8e4',
      'role-pro-300': '#00b7d0',
      'role-pro-400': '#0098aa',
      'role-pro-450': '#008897',
      'role-pro-600': '#005c65',
      'role-pro-700': '#004046',
      'role-pro-800': '#00262a',
      'role-pro-fill': '#008897',
      'role-pro-fill-hover': '#0098aa',
      'role-pro-on': '#000000',
      'role-success-100': '#b0f1ce',
      'role-success-250': '#00d38d',
      'role-success-400': '#009f6a',
      'role-success-450': '#008f5e',
      'role-success-600': '#00603e',
      'role-success-700': '#00442a',
      'role-success-800': '#002817',
      'role-success-fill': '#008f5e',
      'role-success-fill-hover': '#009f6a',
      'role-success-on': '#000000',
      'role-tooltip-bg': '#120a24',
      'role-tooltip-fg': '#ffffff',
      'role-warning-100': '#ffd9a6',
      'role-warning-200': '#ffae43',
      'role-warning-250': '#f9990b',
      'role-warning-300': '#e68c0c',
      'role-warning-600': '#784107',
      'role-warning-700': '#552b04',
      'role-warning-800': '#341801',
      'role-warning-fill': '#ffae43',
      'role-warning-fill-hover': '#f9990b',
      'role-warning-on': '#2b0f2e',
      'text-git-added': '#137a52',
      'text-git-closed': '#b8283c',
      'text-git-conflicting': '#b4500f',
      'text-git-draft': '#6e5f7a',
      'text-git-merged': '#7a3fd1',
      'text-git-modified': '#9a5800',
      'text-git-removed': '#b01e37',
    },
  },
  label: 'Neon Coast',
  v: 1,
}

type Point = readonly [number, number]

const round = (n: number) => Math.round(n * 10) / 10

const pt = ([x, y]: Point) => `${round(x)} ${round(y)}`

const add = ([ax, ay]: Point, [bx, by]: Point, k = 1): Point => [ax + bx * k, ay + by * k]

const unit = ([x, y]: Point): Point => {
  const length = Math.hypot(x, y) || 1

  return [x / length, y / length]
}

const quad = (p0: Point, c: Point, p1: Point, t: number): Point => [
  (1 - t) ** 2 * p0[0] + 2 * (1 - t) * t * c[0] + t ** 2 * p1[0],
  (1 - t) ** 2 * p0[1] + 2 * (1 - t) * t * c[1] + t ** 2 * p1[1],
]

const quadTangent = (p0: Point, c: Point, p1: Point, t: number): Point =>
  unit([2 * (1 - t) * (c[0] - p0[0]) + 2 * t * (p1[0] - c[0]), 2 * (1 - t) * (c[1] - p0[1]) + 2 * t * (p1[1] - c[1])])

const ORIGIN: Point = [0, 0]
const CROWN: Point = [60, -558]
const TRUNK_BEND: Point = [20, -290]

// A tapered, ringed trunk: both edges sampled along one curve, flared at the foot.
const TRUNK = (() => {
  const steps = Array.from({ length: 17 }, (_, i) => i / 16)
  const edge = (side: 1 | -1) =>
    steps.map(t => {
      const [tx, ty] = quadTangent(ORIGIN, TRUNK_BEND, CROWN, t)
      const width = 17 * (1 - t) + 8 + Math.max(0, 0.1 - t) * 90

      return add(quad(ORIGIN, TRUNK_BEND, CROWN, t), [-ty, tx], width * side)
    })
  const left = edge(1)
  const right = edge(-1).reverse()
  const outline = `M${[...left, ...right].map(pt).join('L')}Z`
  const rings = Array.from({ length: 21 }, (_, i) => 0.06 + i * 0.044)
    .map(t => {
      const center = quad(ORIGIN, TRUNK_BEND, CROWN, t)
      const tangent = quadTangent(ORIGIN, TRUNK_BEND, CROWN, t)
      const normal: Point = [-tangent[1], tangent[0]]
      const width = (17 * (1 - t) + 8) * 0.92

      return `M${pt(add(center, normal, width))}Q${pt(add(center, tangent, 5))} ${pt(add(center, normal, -width))}`
    })
    .join('')

  return `<path class="trunk" d="${outline}"/><path class="ring" d="${rings}"/>`
})()

// One pinnate frond along +x: an arched rachis with leaflets that hang toward its tip.
const frondPaths = (length: number, droop: number) => {
  const control: Point = [length * 0.42, -length * 0.26]
  const tip: Point = [length, length * droop]
  const leaflets = Array.from({ length: 18 }, (_, i) => 0.08 + i * 0.051).flatMap(t => {
    const at = quad(ORIGIN, control, tip, t)
    const tangent = quadTangent(ORIGIN, control, tip, t)
    const normal: Point = [-tangent[1], tangent[0]]
    const size = 62 * Math.sin(Math.PI * Math.min(t * 1.15, 1)) ** 0.7 * (1 - 0.35 * t) + 6

    return ([1, -1] as const).map(side => {
      const direction = unit(add(add(add(ORIGIN, normal, 0.75 * side), tangent, 0.7), [0, 1], 0.6))

      return `M${pt(add(at, tangent, -5))}L${pt(add(at, direction, size))}L${pt(add(at, tangent, 5))}Z`
    })
  })

  return `<path class="rachis" d="M0 0Q${pt(control)} ${pt(tip)}"/><path d="${leaflets.join('')}"/>`
}

type Frond = { angle: number; droop: number; isBack: boolean; isMirrored: boolean; length: number }

const FRONDS: readonly Frond[] = [
  { angle: -30, droop: 0.2, isBack: true, isMirrored: false, length: 220 },
  { angle: -30, droop: 0.2, isBack: true, isMirrored: true, length: 210 },
  { angle: -88, droop: 0.1, isBack: true, isMirrored: false, length: 190 },
  { angle: 8, droop: 0.3, isBack: true, isMirrored: true, length: 240 },
  { angle: -58, droop: 0.34, isBack: false, isMirrored: false, length: 250 },
  { angle: -8, droop: 0.42, isBack: false, isMirrored: false, length: 285 },
  { angle: 30, droop: 0.5, isBack: false, isMirrored: false, length: 265 },
  { angle: 62, droop: 0.54, isBack: false, isMirrored: false, length: 215 },
  { angle: -55, droop: 0.36, isBack: false, isMirrored: true, length: 245 },
  { angle: -12, droop: 0.44, isBack: false, isMirrored: true, length: 275 },
  { angle: 28, droop: 0.52, isBack: false, isMirrored: true, length: 250 },
  { angle: 60, droop: 0.54, isBack: false, isMirrored: true, length: 200 },
]


const COCONUTS = [[-10, 10], [9, 14], [0, 24]].map(([cx, cy]) => `<circle class="nut" cx="${cx}" cy="${cy}" r="10"/>`).join('')

type Rect = readonly [x: number, y: number, width: number, height: number]

type PalmPlacement = { isMirrored: boolean; scale: number; x: number }

type Layout = {
  causeway: readonly [from: number, to: number]
  city: { scale: number; x: number }
  height: number
  horizon: number
  palms: readonly PalmPlacement[]
  shimmer: readonly Rect[]
  stars: readonly Point[]
  sun: { cx: number; cy: number; r: number }
  width: number
}

// The wind blows left to right: a gust reaches each palm as it crosses the bay,
// so a palm on a mirrored frame leans the other way to lean the same way on screen.
const GUST_CROSSING_SECONDS = 3.2

const palm = ({ isMirrored, scale, x }: PalmPlacement, layout: Layout) => {
  const gustDelay = (x / layout.width) * GUST_CROSSING_SECONDS
  const frond = (f: Frond, i: number) => {
    const isFlipped = isMirrored !== f.isMirrored
    const frame = `${f.isMirrored ? 'scale(-1 1) ' : ''}rotate(${f.angle})`
    const sway = `animation-duration:${5.6 + ((i * 7) % 5) * 0.6}s;animation-delay:-${(i * 1.7) % 6}s`
    const flutter = `animation-duration:${6 + ((i * 3) % 4) * 0.7}s;animation-delay:-${round((i * 1.3) % 6)}s`

    return `<g class="${f.isBack ? 'back' : 'front'}" transform="${frame}"><g class="${isFlipped ? 'fgust-m' : 'fgust'}" style="animation-delay:${round(gustDelay + 0.25 + i * 0.03)}s"><g class="fsway" style="${sway}"><g class="flutter" style="${flutter}">${frondPaths(f.length, f.droop)}</g></g></g></g>`
  }
  const back = FRONDS.filter(f => f.isBack).map(frond).join('')
  const front = FRONDS.filter(f => !f.isBack).map((f, i) => frond(f, i + 4)).join('')

  return `
<g transform="translate(${x} ${layout.height}) scale(${isMirrored ? -scale : scale} ${scale})">
  <g class="sway" style="animation-delay:-${round(x / 300)}s">
    <g class="${isMirrored ? 'pgust-m' : 'pgust'}" style="animation-delay:${round(gustDelay)}s">
      ${TRUNK}
      <g transform="translate(${pt(CROWN)})">${back}${COCONUTS}${front}</g>
    </g>
  </g>
</g>`
}

// A low dark bank the palm stands on, so it doesn't rise out of open water.
const shore = ({ isMirrored, scale, x }: PalmPlacement, { height }: Layout) => {
  const reach = 320 * scale
  const rise = 46 * scale
  const far = isMirrored ? x - reach : x + reach

  return `<path class="shore" d="M${round(x + (isMirrored ? 60 : -60))} ${height}V${round(height - rise)}Q${round((x + far) / 2)} ${round(height - rise * 1.1)} ${round(far)} ${height}Z"/>`
}

const ROOF = { antenna: 'antenna', deco: 'deco', flat: 'flat', sail: 'sail', step: 'step' } as const

type Roof = (typeof ROOF)[keyof typeof ROOF]

type Tower = { height: number; roof: Roof; width: number; windows: 'a' | 'b'; x: number }

// One downtown cluster, drawn from its own baseline (y 0 is the horizon) with a
// stepped Art Deco hero, a sail-shaped tower and masts, stepping down at both ends.
const TOWERS: readonly Tower[] = [
  { height: 46, roof: ROOF.flat, width: 30, windows: 'a', x: -34 },
  { height: 72, roof: ROOF.flat, width: 34, windows: 'b', x: 0 },
  { height: 112, roof: ROOF.antenna, width: 26, windows: 'a', x: 30 },
  { height: 152, roof: ROOF.step, width: 44, windows: 'b', x: 60 },
  { height: 258, roof: ROOF.deco, width: 56, windows: 'a', x: 108 },
  { height: 196, roof: ROOF.sail, width: 42, windows: 'b', x: 170 },
  { height: 122, roof: ROOF.flat, width: 30, windows: 'a', x: 216 },
  { height: 58, roof: ROOF.flat, width: 64, windows: 'b', x: 250 },
  { height: 92, roof: ROOF.antenna, width: 22, windows: 'a', x: 292 },
]

const FAR_ROW: readonly Rect[] = [
  [-20, -60, 26, 60], [14, -96, 30, 96], [52, -74, 22, 74], [90, -128, 34, 128], [150, -84, 24, 84], [196, -150, 30, 150],
  [236, -102, 26, 102], [270, -70, 34, 70], [312, -48, 30, 48],
]

const rect = ([x, y, width, height]: Rect, cls = '') =>
  `<rect${cls === '' ? '' : ` class="${cls}"`} x="${round(x)}" y="${round(y)}" width="${round(width)}" height="${round(height)}"/>`

const windows = (x: number, top: number, width: number, bottom: number, set: 'a' | 'b') =>
  width > 14 && bottom - top > 14 ? rect([x + 4, top + 6, width - 8, bottom - top - 10], `wins-${set}`) : ''

const tower = ({ height: h, roof, width: w, windows: set, x }: Tower) => {
  switch (roof) {
    case ROOF.deco: {
      const body = h * 0.78
      const tiers = [0, 1, 2].map(i => rect([x + 5 + i * 6, -body - (i + 1) * 15, w - 10 - i * 12, 16])).join('')

      return {
        mass: `${rect([x, -body, w, body])}${tiers}<path class="mast" d="M${x + w / 2} ${round(-body - 45)}V${-h - 26}"/>`,
        neon: `<path class="neon-a" d="M${x} ${round(-body)}H${x + w}M${x + 5} ${round(-body - 15)}H${x + w - 5}M${x + w - 1} ${round(-body)}V0"/>`,
        windows: windows(x, -body, w, 0, set),
      }
    }
    case ROOF.sail:
      return {
        mass: `<path d="M${x} 0V${-h}Q${round(x + w * 1.15)} ${round(-h * 0.45)} ${x + w} 0Z"/>`,
        neon: `<path class="neon-b" d="M${x} ${-h}Q${round(x + w * 1.15)} ${round(-h * 0.45)} ${x + w} 0"/>`,
        windows: windows(x, -h * 0.82, w * 0.62, 0, set),
      }
    case ROOF.step:
      return {
        mass: `${rect([x, -h * 0.8, w, h * 0.8])}${rect([x + w * 0.15, -h, w * 0.7, h * 0.2 + 1])}`,
        neon: '',
        windows: windows(x, -h * 0.8, w, 0, set),
      }
    case ROOF.antenna:
      return {
        mass: `${rect([x, -h, w, h])}<path class="mast" d="M${x + w / 2} ${-h}V${-h - 26}"/>`,
        neon: `<circle class="beacon" cx="${x + w / 2}" cy="${-h - 27}" r="2.4"/>`,
        windows: windows(x, -h, w, 0, set),
      }
    case ROOF.flat:
      return { mass: rect([x, -h, w, h]), neon: '', windows: windows(x, -h, w, 0, set) }
  }
}

const CITY_PARTS = TOWERS.map(tower)

const CITY = `<g class="city-far">${FAR_ROW.map(r => rect(r)).join('')}</g><g class="city">${CITY_PARTS.map(p => p.mass).join('')}</g>${CITY_PARTS.map(p => p.windows).join('')}<g class="neon">${CITY_PARTS.map(p => p.neon).join('')}</g>`

const causeway = ([from, to]: readonly [number, number], horizon: number) => {
  const y = horizon + 9
  const spans = Math.floor((to - from) / 38)
  const piers = Array.from({ length: spans + 1 }, (_, i) => `M${from + i * 38} ${y + 2}v6`).join('')
  const lights = Array.from({ length: spans }, (_, i) => `<circle cx="${from + 19 + i * 38}" cy="${y - 3}" r="1.6" style="animation-delay:-${(i * 1.9) % 8}s"/>`).join('')

  return `<g class="causeway"><rect x="${from}" y="${y}" width="${to - from}" height="2.5"/><path class="pier" d="${piers}"/><g class="cw-lights">${lights}</g></g>`
}

// Sun glitter widens toward the viewer, with spacing that grows with perspective.
const glints = ({ cx, r }: Layout['sun'], horizon: number) => {
  const jitter = [0, 9, -7, 12, -5, 7, -11, 4]
  let y = horizon + 10

  return jitter
    .map((dx, i) => {
      const width = r * 0.85 + i * 9 + Math.abs(dx) * 2
      const out = `<rect class="glint" x="${round(cx - width / 2 + dx)}" y="${y}" width="${round(width)}" height="${3 + i * 0.6}" rx="2" style="animation-delay:-${round(i * 1.1)}s"/>`

      y += 11 + i * 3.5

      return out
    })
    .join('')
}

const STYLE = `<style>
.sky0{stop-color:#ffe3ec}.sky1{stop-color:#ffbccd}.sky2{stop-color:#ffa36e}.sky3{stop-color:#ffd08a}
.sea0{stop-color:#8fd6d9}.sea1{stop-color:#3a8fb5}.sea2{stop-color:#3b3f86}
.fade0{stop-color:#fff;stop-opacity:.42}.fade1{stop-color:#fff;stop-opacity:0}
.trunk{fill:#3d1a4a;stroke:#ffcf7a;stroke-opacity:.3;stroke-width:1.2}
.ring{fill:none;stroke:#6e3c76;stroke-width:1.6;opacity:.75}
.nut{fill:#2a0f33}
.shore{fill:#3d1a4a}
.front path{fill:#3d1a4a;stroke:#ffcf7a;stroke-opacity:.32;stroke-width:1}
.back path{fill:#5e3166;stroke:none}
.rachis{fill:none;stroke-width:5;stroke-linecap:round}
.front .rachis{fill:none;stroke:#3d1a4a;stroke-opacity:1;stroke-width:5}
.back .rachis{fill:none;stroke:#5e3166}
.city{fill:#a84a78}
.city-far{fill:#e39ab4}
.wins-a{fill:url(#wins-a)}.wins-b{fill:url(#wins-b)}
.lit-a,.lit-b{fill:#ffd36b;opacity:.9}
.dim{fill:#7d3561;opacity:.45}
.mast{fill:none;stroke:#a84a78;stroke-width:2}
.neon path{fill:none;stroke:#ffcf7a;stroke-width:2;opacity:.85}
.beacon{fill:#ffcf7a}
.causeway rect{fill:#8a5a9c;opacity:.55}
.pier{stroke:#8a5a9c;stroke-width:2;opacity:.45}
.cw-lights{fill:#fff1c4;opacity:0}
.stars{fill:#fff4fb;opacity:0}
.horizon{fill:#fff3d6;opacity:.7}
.horizon-glow{fill:#ff7aa8;opacity:.35}
.shim{opacity:.45;animation:drift 20s ease-in-out infinite alternate}
.shim.cyan{fill:#e9fdff}.shim.pink{fill:#ffd0e1}
.glint{fill:#fff0b8;opacity:.7;animation:pulse 10s ease-in-out infinite alternate}
.halo{opacity:.5;animation:breathe 14s ease-in-out infinite alternate}
.sway,.pgust,.pgust-m,.fgust,.fgust-m,.fsway,.flutter{transform-origin:0 0}
.sway{animation:sway 11s ease-in-out infinite alternate}
.pgust{animation:pgust 18s infinite}
.pgust-m{animation:pgust-m 18s infinite}
.fgust{animation:fgust 18s infinite}
.fgust-m{animation:fgust-m 18s infinite}
.fsway{animation:fsway 6s ease-in-out infinite alternate}
.flutter{animation:flutter 7s ease-in-out infinite alternate}
.stars circle{animation:twinkle 8s ease-in-out infinite alternate}
@media (prefers-color-scheme: dark){
.sky0{stop-color:#0a0524}.sky1{stop-color:#2d0f5c}.sky2{stop-color:#c21f74}.sky3{stop-color:#ff9a4a}
.sea0{stop-color:#6a1663}.sea1{stop-color:#1c0b3a}.sea2{stop-color:#05020c}
.fade0{stop-opacity:.55}
.trunk{fill:#07030f;stroke:#3ee8ff;stroke-opacity:.22;stroke-width:1.5}
.ring{stroke:#3ee8ff;opacity:.2}
.nut{fill:#12081f}
.shore{fill:#07030f}
.front path{fill:#07030f;stroke:#3ee8ff;stroke-opacity:.16;stroke-width:1}
.back path{fill:#170a2d;stroke:none}
.front .rachis{stroke:#07030f;stroke-opacity:1;stroke-width:5}
.back .rachis{stroke:#170a2d}
.city{fill:#1a0a2e}
.city-far{fill:#2c1550}
.lit-a{fill:#ff4fa3;opacity:.9}.lit-b{fill:#3ee8ff;opacity:.85}
.dim{fill:#2e1a4a;opacity:.8}
.mast{stroke:#1a0a2e}
.neon .neon-a{stroke:#ff4fa3;opacity:1}.neon .neon-b{stroke:#3ee8ff;opacity:1}
.beacon{fill:#ff3d5a;animation:blink 4s ease-in-out infinite alternate}
.causeway rect{fill:#12081f;opacity:1}
.pier{stroke:#12081f;opacity:1}
.cw-lights{opacity:1}.cw-lights circle{fill:#ffd36b;animation:twinkle 8s ease-in-out infinite alternate}
.stars{opacity:1}
.horizon{fill:#ffd36b;opacity:.9}
.horizon-glow{fill:#ff2e88;opacity:.6}
.shim{opacity:.55}
.shim.cyan{fill:#3ee8ff}.shim.pink{fill:#ff4fa3}
.glint{fill:#ff8fbf}
.halo{opacity:.85}
}
@keyframes sway{from{transform:rotate(-1.4deg)}to{transform:rotate(1.4deg)}}
@keyframes fsway{from{transform:rotate(-2deg)}to{transform:rotate(2deg)}}
@keyframes flutter{from{transform:scale(1,.97)}to{transform:scale(1,1.02)}}
@keyframes pgust{0%,60%{transform:rotate(0)}68%{transform:rotate(1.5deg)}74%{transform:rotate(-.6deg)}80%{transform:rotate(.25deg)}87%,100%{transform:rotate(0)}}
@keyframes pgust-m{0%,60%{transform:rotate(0)}68%{transform:rotate(-1.5deg)}74%{transform:rotate(.6deg)}80%{transform:rotate(-.25deg)}87%,100%{transform:rotate(0)}}
@keyframes fgust{0%,60%{transform:rotate(0)}67%{transform:rotate(4deg)}73%{transform:rotate(-1.8deg)}79%{transform:rotate(.8deg)}86%,100%{transform:rotate(0)}}
@keyframes fgust-m{0%,60%{transform:rotate(0)}67%{transform:rotate(-4deg)}73%{transform:rotate(1.8deg)}79%{transform:rotate(-.8deg)}86%,100%{transform:rotate(0)}}
@keyframes drift{from{transform:translateX(-30px)}to{transform:translateX(30px)}}
@keyframes pulse{from{opacity:.4}to{opacity:.8}}
@keyframes breathe{from{opacity:.5}to{opacity:.9}}
@keyframes twinkle{from{opacity:.3}to{opacity:1}}
@keyframes blink{from{opacity:.25}to{opacity:1}}
</style>`

// Window grids: one tile of lit and dark panes, two offsets so neighbours differ.
const windowPattern = (id: string, lit: readonly number[]) => {
  const panes = Array.from({ length: 8 }, (_, i) => {
    const x = 1 + (i % 4) * 6
    const y = 2 + Math.floor(i / 4) * 9

    return `<rect class="${lit.includes(i) ? (i % 2 === 0 ? 'lit-a' : 'lit-b') : 'dim'}" x="${x}" y="${y}" width="2.5" height="5"/>`
  }).join('')

  return `<pattern id="${id}" width="24" height="18" patternUnits="userSpaceOnUse">${panes}</pattern>`
}

const scene = (layout: Layout) => {
  const { city, height, horizon, sun, width } = layout
  const stripes = [0, 1, 2, 3, 4]
    .map(i => `<rect x="${sun.cx - sun.r - 10}" y="${round(sun.cy + 12 + i * 21)}" width="${sun.r * 2 + 20}" height="${round(3.5 + i * 2.4)}" fill="#000"/>`)
    .join('')
  const stars = layout.stars
    .map(([cx, cy], i) => `<circle cx="${cx}" cy="${cy}" r="${i % 3 === 0 ? 2.1 : 1.3}" style="animation-delay:-${(i % 5) * 1.6}s"/>`)
    .join('')
  const shimmer = layout.shimmer
    .map((r, i) => `<rect class="shim ${i % 2 === 0 ? 'cyan' : 'pink'}" x="${r[0]}" y="${r[1]}" width="${r[2]}" height="${r[3]}" rx="1.5" style="animation-delay:-${round(i * 1.9)}s"/>`)
    .join('')
  const cityAt = `translate(${city.x} ${horizon}) scale(${city.scale})`

  return `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 ${width} ${height}" preserveAspectRatio="xMidYMid slice">
${STYLE}
<defs>
<linearGradient id="sky" x1="0" y1="0" x2="0" y2="1">
<stop offset="0" class="sky0"/><stop offset=".45" class="sky1"/><stop offset=".85" class="sky2"/><stop offset="1" class="sky3"/>
</linearGradient>
<linearGradient id="sea" x1="0" y1="0" x2="0" y2="1">
<stop offset="0" class="sea0"/><stop offset=".35" class="sea1"/><stop offset="1" class="sea2"/>
</linearGradient>
<linearGradient id="sun" x1="0" y1="0" x2="0" y2="1">
<stop offset="0" stop-color="#ffe066"/><stop offset=".5" stop-color="#ff8a4c"/><stop offset="1" stop-color="#ff2e88"/>
</linearGradient>
<radialGradient id="halo">
<stop offset="0" stop-color="#ff4f9a" stop-opacity=".7"/><stop offset=".5" stop-color="#ff7a3d" stop-opacity=".25"/><stop offset="1" stop-color="#ff7a3d" stop-opacity="0"/>
</radialGradient>
<linearGradient id="fade" x1="0" y1="0" x2="0" y2="1">
<stop offset="0" class="fade0"/><stop offset="1" class="fade1"/>
</linearGradient>
<filter id="glow" x="-10%" y="-400%" width="120%" height="900%">
<feGaussianBlur stdDeviation="7"/>
</filter>
<mask id="stripes" maskUnits="userSpaceOnUse" x="0" y="0" width="${width}" height="${height}">
<rect x="0" y="0" width="${width}" height="${height}" fill="#fff"/>${stripes}
</mask>
<mask id="reflection" maskUnits="userSpaceOnUse" x="0" y="${horizon}" width="${width}" height="${round(170 * city.scale)}">
<rect x="0" y="${horizon}" width="${width}" height="${round(170 * city.scale)}" fill="url(#fade)"/>
</mask>
${windowPattern('wins-a', [1, 4, 6])}
${windowPattern('wins-b', [2, 3, 7])}
</defs>
<rect width="${width}" height="${horizon}" fill="url(#sky)"/>
<g class="stars">${stars}</g>
<circle class="halo" cx="${sun.cx}" cy="${sun.cy}" r="${round(sun.r * 2.4)}" fill="url(#halo)"/>
<circle cx="${sun.cx}" cy="${sun.cy}" r="${sun.r}" fill="url(#sun)" mask="url(#stripes)"/>
<g transform="${cityAt}">${CITY}</g>
<rect y="${horizon}" width="${width}" height="${height - horizon}" fill="url(#sea)"/>
<g mask="url(#reflection)"><g transform="translate(${city.x} ${horizon}) scale(${city.scale} ${-city.scale * 0.62})">${CITY}</g></g>
<rect class="horizon-glow" y="${horizon - 10}" width="${width}" height="20" filter="url(#glow)"/>
<rect class="horizon" y="${horizon - 1}" width="${width}" height="2"/>
${causeway(layout.causeway, horizon)}
${glints(sun, horizon)}
${shimmer}
${layout.palms.map(p => shore(p, layout)).join('')}
${layout.palms.map(p => palm(p, layout)).join('')}
</svg>`
}

// Desktop: the chat column covers the middle half of the window, so the city
// holds the left band, the sun and its palm the right band, and the middle is
// left to the glow, the causeway and the water.
const WIDE_SCENE = scene({
  causeway: [400, 1170],
  city: { scale: 0.9, x: 140 },
  height: 1000,
  horizon: 640,
  palms: [
    { isMirrored: false, scale: 0.8, x: -10 },
    { isMirrored: true, scale: 0.95, x: 1610 },
  ],
  shimmer: [
    [900, 660, 140, 3], [1060, 672, 110, 3], [1190, 688, 80, 3], [1440, 668, 110, 3], [760, 702, 150, 3],
    [1250, 722, 70, 3], [980, 742, 190, 3], [1400, 764, 120, 3], [430, 706, 150, 3], [560, 752, 130, 3],
  ],
  stars: [
    [140, 60], [310, 140], [520, 40], [700, 110], [880, 70], [1040, 150], [1220, 50], [1400, 110], [1530, 64],
    [230, 220], [610, 200], [960, 236], [80, 170], [800, 180],
  ],
  sun: { cx: 1300, cy: 560, r: 150 },
  width: 1600,
})

// Phone: the chat covers the whole width, so the scene keeps to the top third
// and the corners: the sun high on the left behind the towers, one palm reaching
// in from the right edge.
const TALL_SCENE = scene({
  causeway: [330, 900],
  city: { scale: 0.92, x: 40 },
  height: 1600,
  horizon: 640,
  palms: [{ isMirrored: true, scale: 1.75, x: 930 }],
  shimmer: [
    [210, 660, 120, 3], [390, 674, 90, 3], [560, 690, 140, 3], [260, 718, 160, 3], [90, 760, 110, 3],
    [430, 792, 130, 3], [640, 834, 100, 3], [300, 884, 150, 3],
  ],
  stars: [[60, 60], [180, 140], [420, 40], [560, 120], [700, 60], [820, 170], [120, 250], [640, 240], [360, 200]],
  sun: { cx: 300, cy: 500, r: 125 },
  width: 900,
})

const LOOK: ThemeSetArgs = {
  backdrop: { glass: { blur: 20, opacity: 0.55 }, scene: SCENE_NAME },
  colors: COLORS,
}

export const register: Register = on => {
  on('session.start', async ($, e, next) => {
    const set = await $.theme.set(LOOK)

    if (!set.isDrawn) {
      $.ui.status(set.reason)
    }

    return next(e)
  })

  on('ui.render', { component: 'Backdrop' }, ($, e, next) => {
    if ((e.surface !== 'desktop' && e.surface !== 'mobile') || e.props.scene !== SCENE_NAME) {
      return next(e)
    }
    const { Svg } = $.ui.resolve(e)
    const source = e.surface === 'mobile' ? TALL_SCENE : WIDE_SCENE

    return <Svg alt="A neon sunset over a tropical bay: an Art Deco skyline and its causeway, palms swaying as gusts cross the water" source={source} />
  })
}
```

### 2. Check that it was copied correctly (optional)

```bash
claude plugin validate ~/claude-themes/neon-coast
```

It should end with `Validation passed`. Warnings about `author` don't matter. If your Claude Code is older than the app, it may warn that `Backdrop` doesn't exist. That warning doesn't matter either, as long as the app is up to date.

### 3. Activate it

**Method A (recommended): install it as a plugin from the folder.**

```bash
claude plugin marketplace add ~/claude-themes/neon-coast
```

```bash
claude plugin install neon-coast@neon-coast
```

From the desktop app, without a terminal: tap **+** next to the message box → **Plugins** → **Add marketplace**, paste the folder path, and then **Add plugin** → `neon-coast`.

**Method B: load it directly from the folder.** Add this to `~/.claude/settings.json`. If the file already has an `env` block, just add the one line:

```json
{
  "env": {
    "CLAUDE_CODE_PLUGIN_DIRS": "~/claude-themes/neon-coast"
  }
}
```

### 4. See it

Open a **new session** in the app. The theme is applied when the session starts. Try both modes (light and dark) from the app's appearance settings.

## Details

- **Reduce motion:** if you have "reduce motion" turned on in your system, the app shows the scene still, in a complete resting pose.
- **Legibility:** the conversation panels are drawn with a frosted glass over the background (blur 20, opacity 0.55). You change it in the code at `LOOK.backdrop.glass`.
- **Turning it off:** with method A, `claude plugin uninstall neon-coast`. With method B, remove the line from `settings.json`. In both cases, open a new session.

## Customizing it

Everything is in `hooks/register.tsx`:

| You want to change | Where |
|---|---|
| Position and size of the sun, the city, the palms and the causeway (desktop) | `WIDE_SCENE` |
| The same on mobile | `TALL_SCENE` |
| Shape and height of the buildings | `TOWERS` and `FAR_ROW` |
| Colors of the sky, the sea, the neon and the silhouettes | The `STYLE` block: light mode at the top, dark mode inside `@media (prefers-color-scheme: dark)` |
| Speed and strength of the wind | The `@keyframes` `pgust`/`fgust` (gusts), `sway`/`fsway` (sway) and `flutter` (leaflets) |
| Interface colors (surfaces, text, accent) | `COLORS`, which is precomputed. To regenerate it, ask Claude Code to use the `plugin-authoring` skill |

If you change it with method A, after editing run `/reload-plugins` in a session or open a new one.

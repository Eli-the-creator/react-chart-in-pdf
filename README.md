# react-chart-in-pdf
My old npm package - wraper for "React-PDF" what add new component for render "recharts" in to PDF


## The problem

One of the best ways to generate PDFs is using [`react-pdf`](https://react-pdf.org/). Unfortunately `react-pdf` has [several](https://github.com/diegomura/react-pdf/issues/1720) [major](https://github.com/diegomura/react-pdf/issues/1271) [annoying](https://github.com/diegomura/react-pdf/issues/2003) [bugs](https://github.com/diegomura/react-pdf/issues/2017) that makes rendering SVG charts very difficult. This library attempts to ease the pain and provide a possible workaround until those bugs are fixed.

## This solution

This library provides a wrapper component that allows you to use popular SVG charting libraries (like `recharts`) in your `react-pdf` PDF documents. The wrapper will convert all generated `<svg>` DOM elements into compatible [`react-pdf` SVG image elements](https://react-pdf.org/svg). The library will also attempt to workaround common bugs and limitations gracefully.


## Installation

This module is distributed via [npm][npm] which is bundled with [node][node] and
should be installed as one of your project's `dependencies`:

```
npm install 
```

## Usage

```tsx
import ReactPDFChart from "react-pdf-charts";

const data = [
  {
    name: "Page A",
    uv: 4000,
    pv: 2400,
    amt: 2400,
  },
  {
    name: "Page B",
    uv: 3000,
    pv: 1398,
    amt: 2210,
  },
  {
    name: "Page C",
    uv: 2000,
    pv: 9800,
    amt: 2290,
  },
  {
    name: "Page D",
    uv: 2780,
    pv: 3908,
    amt: 2000,
  },
  {
    name: "Page E",
    uv: 1890,
    pv: 4800,
    amt: 2181,
  },
  {
    name: "Page F",
    uv: 2390,
    pv: 3800,
    amt: 2500,
  },
  {
    name: "Page G",
    uv: 3490,
    pv: 4300,
    amt: 2100,
  },
];

const SomeComponent = () => (
  <ReactPDFChart>
    <LineChart data={data} height={300} width={500}>
      <XAxis dataKey="name" />
      <YAxis />
      <CartesianGrid stroke="#eee" strokeDasharray="5" />
      <Line type="monotone" dataKey="uv" stroke="#8884d8" />
      <Line type="monotone" dataKey="pv" stroke="#82ca9d" />
    </LineChart>
  </ReactPDFChart>
);
```

From there you can pass `SomeComponent` to `react-pdf` to be rendered either on the server or the client via its rendering APIs.

## Props

### debug

> `boolean` | defaults to `false`

Enables `react-pdf` [debugging mode](https://react-pdf.org/advanced#debugging) for the outer wrapper element.

### chartStyle

> `{}` | optional, some base `recharts` styles are applied by default

An optional [Stylesheet](https://react-pdf.org/styling) that maps web CSS class names to whatever `react-pdf` styles you wish to replace those classes with.

The idea is that popular SVG charting libraries (like `recharts`) will apply various classes to its elements (eg. `<span class="recharts-default-legend">...</span>`). Since class names aren't supported in `react-pdf`, this prop allows to you replace those class names with custom styling. The `react-pdf-charts` library will convert any matches class names to the corresponding `react-pdf` styles.

### style

> `{}` | optional, no default

An optional [style](https://react-pdf.org/styling) that will get applied to the outer element of the wrapper component.


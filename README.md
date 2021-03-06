![Chart Kit](https://i.imgur.com/Idp4WIX.jpg)

# React Native Chart Kit Documentation

## Import components
1. Place the folder with the project in your working directory
2. Use with ES6 syntax to import components

```js
import LineChart from 'react-native-graph-kit/src/line-chart'
import BarChart from 'react-native-graph-kit/src/bar-chart'
import PieChart from 'react-native-graph-kit/src/pie-chart'
import Progress from 'react-native-graph-kit/src/progress-chart'
import LineChart from 'react-native-graph-kit/src/contribution-graph'
```

## Chart style object
Define a chart style object with following properies as such:
```js
const chartConfig = {
  backgroundGradientFrom: '#1E2923',
  backgroundGradientTo: '#08130D',
  color: (opacity = 1) => `rgba(26, 255, 146, ${opacity})`
}
```

| Property        | Type           | Description  |
| ------------- |-------------| -----|
| backgroundGradientFrom | string | Defines the first color in the linear gradient of a chart's background  |
| backgroundGradientTo | string | Defines the second color in the linear gradient of a chart's background |
| color | function => string | Defines the base color function that is used to calculate colors of labels and sectors used in a chart |

## Responsive charts
To render a responsive chart, use `Dimensions` react-native library to get the width of the screen of your device like such
```js
import { Dimensions } from 'react-native'
const screenWidth = Dimensions.get('window').width
```

## Line Chart

![Line Chart](https://i.imgur.com/Wt26snd.jpg)

```js
const data = {
  labels: ['January', 'February', 'March', 'April', 'May', 'June'],
  datasets: [{
    data: [ 20, 45, 28, 80, 99, 43 ]
  }]
}
```

```html
<LineChart
  data={data}
  width={screenWidth}
  height={220}
  chartConfig={chartConfig}
/>
```

| Property        | Type           | Description  |
| ------------- |-------------| -----|
| data | Object | Data for the chart - see example above |
| width | Number | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive |
| height | Number | Height of the chart |
| chartConfig | Object | Configuration object for the chart, see example config object above |

## Bezier Line Chart

![Line Chart](https://i.imgur.com/EnUiZZU.jpg)

```html
<LineChart
  data={data}
  width={screenWidth}
  height={220}
  chartConfig={chartConfig}
  bezier
/>
```

| Property        | Type           | Description  |
| ------------- |-------------| -----|
| bezier | boolean | Add this prop to make the line chart smooth and curvy |

## Progress Ring

![Progress Chart](https://i.imgur.com/U4lkW0K.jpg)

```js
// each value represents a goal ring in Progress chart
const data = [0.4, 0.6, 0.8]
```

```html
<ProgressChart
  data={data}
  width={screenWidth}
  height={220}
  chartConfig={chartConfig}
/>
```
| Property        | Type           | Description  |
| ------------- |-------------| -----|
| data | Object | Data for the chart - see example above |
| width | Number | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive |
| height | Number | Height of the chart |
| chartConfig | Object | Configuration object for the chart, see example config in the beginning of this file |

## Bar chart

![Bat Chart](https://i.imgur.com/jVHEWiI.jpg)

```js
const data = {
  labels: ['January', 'February', 'March', 'April', 'May', 'June'],
  datasets: [{
    data: [ 20, 45, 28, 80, 99, 43 ]
  }]
}
```
```html
<BarChart
  style={graphStyle}
  data={data}
  width={screenWidth}
  height={220}
  chartConfig={chartConfig}
/>
```

| Property        | Type           | Description  |
| ------------- |-------------| -----|
| data | Object | Data for the chart - see example above |
| width | Number | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive |
| height | Number | Height of the chart |
| chartConfig | Object | Configuration object for the chart, see example config in the beginning of this file |

## Pie chart

![Pie Chart](https://i.imgur.com/JMz3obk.jpg)

```js
const data = [
  { name: 'Toronto', population: 2800000  },
  { name: 'Dublin', population: 527612 },
  { name: 'New York', population: 8538000 },
  { name: 'Beijing', population: 21500000 },
  { name: 'Moscow', population: 11920000 }
]
```
```html
<PieChart
  data={data}
  width={screenWidth}
  height={220}
  chartConfig={chartConfig}
  accessor="population"
/>
```

| Property        | Type           | Description  |
| ------------- |-------------| -----|
| data | Object | Data for the chart - see example above |
| width | Number | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive |
| height | Number | Height of the chart |
| chartConfig | Object | Configuration object for the chart, see example config in the beginning of this file |
| accessor | string | Property in the `data` object from which the number values are taken |

## Contribution graph (heatmap)

![Contribution Graph](https://i.imgur.com/NKURRt6.jpg)

This type of graph is often use to display a developer contribution activity. However, there many other use cases this graph is used when you need to visualize a frequency of a certain event over time.

```js
const commitsData = [
  { date: '2017-01-02', count: 1 },
  { date: '2017-01-03', count: 2 },
  { date: '2017-01-04', count: 3 },
  { date: '2017-01-05', count: 4 },
  { date: '2017-01-06', count: 5 },
  { date: '2017-01-30', count: 2 },
  { date: '2017-01-31', count: 3 },
  { date: '2017-03-01', count: 2 },
  { date: '2017-04-02', count: 4 },
  { date: '2017-03-05', count: 2 },
  { date: '2017-02-30', count: 4 }
]
```

```html
<ContributionGraph
  values={commitsData}
  endDate={new Date('2017-04-01')}
  numDays={105}
  width={screenWidth}
  height={220}
  chartConfig={chartConfig}
/>
```

| Property        | Type           | Description  |
| ------------- |-------------| -----|
| data | Object | Data for the chart - see example above |
| width | Number | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive |
| height | Number | Height of the chart |
| chartConfig | Object | Configuration object for the chart, see example config in the beginning of this file |
| accessor | string | Property in the `data` object from which the number values are taken |

## More styling
Every charts also accepts `style` props, which will be applied to parent `svg` or `View` component of each chart.

## Abstract Chart

`src/abstract-chart.js` is an extendable class which can be used to create your own charts!

The following methods are available:

### renderHorizontalLines(config)
Renders background horizontal lines like in the Line Chart and Bar Chart. Takes a config object with following properties:
```js
{
  // width of your chart
  width: Number,
  // height of your chart
  height: Number,
  // how many lines to render
  count: Number,
  // how many labels there will be on X axes - used to calculate offsets between the lines
  labelCount: Number,
  // top padding from the chart top edge
  paddingTop: Number
}
```

### renderVerticalLabels(config)
Render background vertical lines. Takes a config object with following properties:
```js
{
  // data needed to calculate the number of lines to render
  data: Array,
  // width of your chart
  width: Number,
  // height of your chart
  height: Number,
  paddingTop: Number,
  paddingRight: Number
}
```

### renderDefs(config)
Render definitions of background and shadow gradients
```js
{
  // width of your chart
  width: Number,
  // height of your chart
  height: Number,
  // first color of background gradient
  backgroundGradientFrom: String,
  // second color of background gradient
  backgroundGradientTo: String
}
```

## More information
This library is built on top of the following open-source projects:
* react-native-svg (https://github.com/react-native-community/react-native-svg)
* paths-js  (https://github.com/andreaferretti/paths-js)
* react-native-calendar-heatmap (https://github.com/ayooby/react-native-calendar-heatmap)

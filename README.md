# Grafana Plugins

A suite of plugins for [Grafana](http://grafana.org/).

![Grafana Plugins](https://raw.githubusercontent.com/BTplc/grafana-plugins/master/readme.png)

## Plugins

This repo contains the following plugins. Each plugin should work with the datasources specified in brackets after the name.

### Alarm Box (Elasticsearch, Graphite)

A box panel that displays the total count of values across all series. This is useful if you want to show a total count of alarms. Options for this panel include variable font sizes (title and number) and color thresholds for the number.

![Alarm Box Panel](https://raw.githubusercontent.com/BTplc/grafana-plugins/master/alarm_box/src/img/alarm_box.png)

### Peak Report (Graphite)

A table panel that summarises multiple series into a report of peak values. Each row is formed by grouping series together using the first few components of the metric name. The cells for a row are calculated using some or all of the series, filtered by regex. The value for a cell is the maximum or peak value across all the series matching the regex filter for the column.

![Peak Report Panel](https://raw.githubusercontent.com/BTplc/grafana-plugins/master/peak_report/src/img/peak_report_tutorial.gif)

### Trend Box (Graphite)

A box panel that displays the percentage change between the first and last values of a series. This is useful if you want to to monitor a value as it changes over time. The panel can also work with multiple series by adding together the values at each end. Options for this panel include variable font sizes, precision, units and color thresholds for the percentage change.

![Trend Box Panel](https://raw.githubusercontent.com/BTplc/grafana-plugins/master/trend_box/src/img/trend_box.png)

### Trend Dot (Graphite)

A panel that displays a dot for each series, where each dot is colored based on the percentage change between the first and last values of that series. This is is useful if you want to monitor a collection of values as they change over time. Options for this panel include variable radius, precision and units (for the tooltip) and color thresholds for the percentage change.

![Trend Dot Panel](https://raw.githubusercontent.com/BTplc/grafana-plugins/master/trend_dot/src/img/trend_dot.png)

## Development

[Docker](https://www.docker.com/) is an easy way to spin-up an instance of Grafana. With docker installed, run the following command in the directory containing all the plugins; this will expose the local plugins to the Grafana container so you can test them out.

    docker run -it -v $PWD:/var/lib/grafana/plugins -p 3000:3000 --name grafana.docker grafana/grafana

To work on a particular plugin, do this.

    # Work on my_plugin
    cd my_plugin
    # Install development plugins
    npm install
    # Compile into dist/
    grunt
    # Restart Grafana to see my_plugin
    docker restart grafana.docker
    # Watch for changes (requires refresh)
    grunt watch

Use `grunt test` to run the Jasmine tests for the plugin; and `grunt eslint` to check for style issues. Note that the plugin controllers aren't tested because they depend on Grafana native libraries, which aren't available outside of Grafana.

## Contributing

For bugs and new features, open an issue and we'll take a look. If you want to contribute to the existing plugins, you're welcome to submit a pull request - just make sure `grunt` runs without errors first.


## Deployment

This repo includes a `deploy` script, which we use to deploy the plugins internally. It requires key-based root login to the server running the Grafana container. The script is just a temporary measure until we can host our plugins on the [community repo](https://grafana.net/).

    ./deploy my_plugin host_dns_or_ip

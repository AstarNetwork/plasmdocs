# Launch and Active Services

##  Launch and Active Services

Launch a **daemon reload** to take the services into account in `systemd`:

```text
sudo systemctl daemon-reload
```

Start the services:

```text
sudo systemctl start prometheus.service
sudo systemctl start node_exporter.service
sudo systemctl start process-exporter.service
sudo systemctl start alertmanager.service
sudo systemctl start grafana-server
```

And check that they are working fine, one by one:

```text
systemctl status prometheus.service
systemctl status node_exporter.service
systemctl status process-exporter.service
systemctl status alertmanager.service
systemctl status grafana-server
```

A service working fine should look like this:

![](../../../.gitbook/assets/image%20%2819%29.png)

When everything is okay, activate the services!

```text
sudo systemctl enable prometheus.service
sudo systemctl enable node_exporter.service
sudo systemctl enable process-exporter.service
sudo systemctl enable alertmanager.service
sudo systemctl enable grafana-server
```

## Test Alert manager <a id="ac61"></a>

Run this command to fire an alert:

```text
curl -H "Content-Type: application/json" -d '[{"labels":{"alertname":"Test"}}]' localhost:9093/api/v1/alerts
```

Check your inbox, you have a surprise:

![](https://miro.medium.com/max/630/1*ZwXa8SNzmoBsAwz_UqnJmw.png)

You will always receive a **Firing** alert first, then a **Resolved** notification to indicate the alert isn’t active anymore.

## Run Grafana dashboard <a id="acc1"></a>

Now is the time to get the most visual part: the **monitoring dashboard**.

From the browser on your local machine, connect to the custom port on localhost that we have set at the beginning of this guide:

```text
http://localhost:2022
```

![](https://miro.medium.com/max/583/1*OqSPo8X5bAQ6Mz-D2j6hSA.png)

Enter the default user `admin` and password `admin` then change the password.

![](https://miro.medium.com/max/1500/0*qTsBUdvIdSXnFR5I.png)

### Add data Sources <a id="e6fc"></a>

Open the _Settings_ menu:

![](https://miro.medium.com/max/250/0*PWZ6IrqONqj-XGDh.png)

Click on _Data Sources_:

![](https://miro.medium.com/max/2000/0*7L1CGXukNlVQ0WrF.png)

Click on Add data source:

![](https://miro.medium.com/max/970/1*8wktdu3VjVI47q26dEXWyQ.png)

Select Prometheus:

![](https://miro.medium.com/max/708/1*6Lpgqtcwq4-tJhPOWAVrXQ.png)

Just fill the URL with http://localhost:9090 and click _Save & Test_.  
Then add a new data source and search for Alert Manager

![](https://miro.medium.com/max/975/1*59LLXEyWtwee93s7C1N_lw.png)

Fill the URL with http://localhost:9093 and click _Save & Test_.

![](https://miro.medium.com/max/665/1*Xs6T8A-qXOPMnW6a38he-Q.png)

Now you have your 2 data sources set like that:

![](https://miro.medium.com/max/968/1*iB3W7iHf8erWBxRLKDLXsQ.png)

### Import the dashboard <a id="7c3d"></a>

Open the _New_ menu:

![](https://miro.medium.com/max/206/1*whppeAr3TPlXUf6dO7t5IQ.png)

Click on _Import_:

![](https://miro.medium.com/max/658/1*Z_hztNvh-WsW7jHOgS0S2w.png)

Select our favorite [dashboard 13840](https://grafana.com/grafana/dashboards/13840), we recommend using this dashboard because it's created by one of our Ambassadors and we don't want to fork this.  All credits goes to him.

![](https://miro.medium.com/max/690/1*_3TVS7AmImGV41_-qUBIog.png)

Select the Prometheus and AlertManager sources and click _Import_.Dashboard selection

![](https://miro.medium.com/max/700/1*n7NH8E8rUhQhlyzqr-WBQQ.png)

In the dashboard selection, make sure you select:

* **Chain Metrics**: `polkadot` for a Polkadot/Kusama node, `substrate` for any other parachain node
* **Chain Instance Host:** `localhost:9615` to point the chain data scrapper
* **Chain Process Name**: the name of your node binary

And here you go, everything is set!

Monitoring dashboard [Polkadot Essentials](https://grafana.com/grafana/dashboards/13840)

![](https://miro.medium.com/max/1856/1*8k0lOw8fTKM8QIzqrYOeUg.jpeg)

Easy right? Just think about saving the dashboard once parameters are set and work.

**Note**: you can also consider [Parity’s dashboards](https://github.com/paritytech/substrate/tree/master/.maintain/monitoring/grafana-dashboards) for advanced monitoring and analysis.




# srt-stats-plotting

<p align="left">
<a href="https://github.com/python/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
</p>

**`srt-stats-plotting`** is a script designed to plot graphs based on SRT core statistics.

[SRT](https://github.com/Haivision/srt) stands for Secure Reliable Transport and is an open source transport technology that optimizes streaming performance across unpredictable networks, such as the Internet.

## Requirements

* python 3.6+
* PhantomJS 2.1 — used to [export plots](https://bokeh.pydata.org/en/latest/docs/user_guide/export.html) (optional)

To install the library dependencies run:
```
pip install -r requirements.txt
```

## Script Usage

The main purpose of the `plot_srt_stats.py` script is to visualize all the SRT core statistics produced during experiments performed using one of the [testing applications](https://github.com/Haivision/srt/blob/master/docs/stransmit.md) or third-party solutions supporting the SRT protocol. Depending on whether these statistics are collected on the sender or receiver side, the data plot may vary.

SRT core statistics should be collected in a `.csv` file. The recommended naming convention for file names is to add the suffix "-snd" or "-rcv" depending on where the data was collected (on the sender or receiver). Alternatively, the file name can just contain "snd" or "rcv".

The statistics file path is passed as an argument to the script:
```
plot_srt_stats.py [OPTIONS] STATS_FILEPATH
```

Use the `--help` option to get the full list of options:
```
--is-sender   Should be set if sender statistics is provided. Otherwise, it
              is assumed that receiver statistics is provided.
--is-fec      Should be set if packet filter (FEC) stats is enabled.
--export-png  Export plots to .png files.
--help        Show this message and exit.
```



## Example Plots

The script plots different charts from SRT statistics. For example, here is an example of a chart that presents statistics on the packets being sent, lost, retransmitted, dropped or on flight:

<img src="img/packets_1.png" alt="packets_1" style="zoom:50%;" />

The legends are interactive. For example, you can click on `Dropped` and `On Flight` to disable the respective plots:

<img src="img/packets_2.png" alt="packets_2" style="zoom:50%;" />

In this example, the chart illustrates the sending rate in Mbps:

<img src="img/sending_rate_mbps.png" alt="sending_rate_mbps" style="zoom:50%;" />

**Note:** The correlation between *megabytes* and *rate* is determined by the following formula:

_Rate (Mbps) = MB / interval (s),_

where _interval_ specifies how frequently the statistics are collected (in seconds).


In this example, the chart shows the available size of the sender's buffer, which helps to detect if there is enough space to store outgoing data, or if the source generates data faster then SRT can transmit:

<img src="img/available_snd_buffer_size.png" alt="available_snd_buffer_size" style="zoom:50%;" />

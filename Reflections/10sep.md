# Reflection of 10 September

In today’s class, I learned about the difference between **file transfer and streaming**. We also revisited the concepts of **population mean (μ)** and **sample mean (\(\bar{x}\))**, along with the problem of estimating variance when working with extremely large datasets.

## File Transfer vs. Streaming

One of the concepts that stood out to me was the difference between **file-based processing and streaming**.

In traditional file transfer, the data has a definite beginning and end, and the complete file is available as a known object. In contrast, **streaming** can be thought of as data continuously arriving over time. The viewer or program does not necessarily need to know when the data will end. This makes streaming particularly useful when dealing with very large or continuously generated datasets.

I understood streaming as a **“data comes → process it immediately → forget it”** approach. Instead of storing the entire dataset in memory, we can process each piece of data as it arrives. This makes streaming more **memory efficient**, especially when the amount of data is too large to fit comfortably into memory.

It also made me realize that streaming is not necessarily about transferring a file faster. Instead, it is about **changing how we handle data**: we process information incrementally rather than waiting for the entire dataset to arrive first.

## Population Mean and Sample Mean

Another important topic was the distinction between the **population mean (μ)** and the **sample mean (\(\bar{x}\))**.

* **Population mean (μ):** The actual average of all the values in an entire population.
* **Sample mean (\(\bar{x}\)):** The average calculated from a sample taken from that population.

This distinction becomes important when the entire population is too large to work with directly. For example, if we have **one trillion data points**, calculating the exact population mean may be impractical. Instead, we can take a representative sample and use its sample mean to estimate the population mean.

## Estimating Variance in Large Datasets

This led to another interesting question for me: **if we can estimate the mean from a huge dataset, how do we estimate its variance?**

The same general idea applies, but variance requires us to keep track of additional information about how individual values differ from the mean. In a streaming scenario, this becomes particularly interesting because we want to calculate statistics such as the **mean and variance without storing all one trillion data points**.

This shows how statistical calculations can become more challenging when the dataset is extremely large. Instead of simply storing everything and calculating the result afterward, we need methods that can process the data **incrementally and efficiently**.

## Overall Reflection

Overall, today’s class helped me connect **statistical concepts with computer science concepts**. I could see how streaming is not just about data transmission, but also about **efficient computation and memory usage**.

The connection between statistics and streaming algorithms made me realize that even something as simple as calculating an average becomes a more interesting problem when the dataset is extremely large. It showed me how computer science techniques can be used to make statistical computation practical for real-world, large-scale datasets.

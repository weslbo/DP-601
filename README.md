# DP-601 Resources

## Create a lakehouse

Create a new lakehouse called `dp601lake`

## Upload notebooks

1. Navigate to https://app.fabric.microsoft.com/home?experience=data-engineering, make sure you're in the correct workspace and click on Import notebook. (There is currenly no API/PowerShell command available to automate this).

![import-notebook](./images/import-notebook.png)

1. Import the notebooks from the `notebooks` folder (you can select multiple files at once 😉)

1. Run the 00-Setup notebook. It will copy some data from github into the lakehouse.

## Explore the dataflow demo

1. Explore the dataflow demo as provided [here](./demo/dataflows.md)
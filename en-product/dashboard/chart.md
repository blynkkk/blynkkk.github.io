   
      Chart is used to visualise live and historical data. You can use it for sensor data, for binary event logging and more. 
  
 SETUP:
- **Add source** – it's possible to set several Datastream **Sources** under one Chart. Click and set up as much as you need.
  
- **Chart Title** – name a chart so you or your client understand what it's about  
- **Source Label** – . The easiest way to name them is giving used Datastreams names.  
- **Source** – there are two fields:  
     - the  right one contains ***Datastreams used in the Product***. Select one;  
     - the left is ***Source agregation type menu*** it's used to select an option to be used in chart data plotting:  
       **AVG of** will plot average value per minute;  
       **Raw of** data will plot using all the data available;  
       **SUM of** will summarize all incoming values to the specified Virtual Pin;  
       **MIN of** will plot minimum value per minute;  
       **MAX of** will plot maximum value per minute;  
       **COUNT of** will plot the number of times data was sent by device per minute;  
- **Chart type:**  - 4 types are available: Line, Area, Column, Stepline. Pick a color to make it different from other sources may use under this chart.  
    - **Show Y-axis** – enable if it's needed to view Datastream values on the axis (X-axis displays the time);  
    - **Autoscale** – enable if there's no specific limitations of the data values needed to be viewed. Otherwise specify them by setting the values in **MIN** and **MAX** fields.
- **Enable zoom** – enable if chart zoom may be useful. Otherwise leave it disabled.

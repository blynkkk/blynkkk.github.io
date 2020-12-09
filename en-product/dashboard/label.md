
      Label is used to show value of Virtual Pin e.g. length/distance, mass, duration, volume, temperature and other data types including strings.

 SETUP: 
- **Label** – name a Label widget so you or your client understand what it's about    
- **Source** – there are two fields:  
     - **Choose Source** contains ***Datastreams used in the Product***. Select one;  
     - the left is ***Source agregation type menu*** it's used to select an option to be viewed:  
       **AVG of** will plot average value per minute;  
       **Raw of** data will plot using all the data available;  
       **SUM of** will summarize all incoming values to the specified Virtual Pin;  
       **MIN of** will plot minimum value per minute;  
       **MAX of** will plot maximum value per minute;  
       **COUNT of** will plot the number of times data was sent by device per minute;  
- **SUFFIX** – inches, lbs, oz, minutes, °F, etc., that will be shown after the value;
- **TEXT ALIGNMENT** – 3 options are available: Left, Center, Right;
- **Background** 
    - disabled **Change color based on value**:
      - **Background** – pick a color for Label widget background from palette or define it by color number input
      - **Text** – same here;
    - enabled **Change color based on value**:
      - set **MIN** and **MAX** values and Background and Font colors (as it's described in previous paragraph);
      - **CUSTOM TEXT (OPTIONAL)** – value can be replaced by any text message up to 200 characters (be sure to set corresponding Label widget size);
      - default set is of 3 options and it can be changed in range from 1 to as much as you need:
        - click **+** button under the last MIN field to ***increase*** set;
        - hover to the right from CUSTOM TEXT field, ***Delete*** button will appear;
- **Level** – enable it by turn on **Show level** switch to visualize accordingly to values set in **MIN and MAX Value** fields below.

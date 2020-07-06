### Info: Template ID  

Product's Template ID is used to check if new Device is allowed to work with the Product's settings.  
  
Follow these steps to allow the Device to use Product's Template you need: 
- select the Product, open Info tab and copy it's Template ID (several Template IDs can be assigned to one Product);
- in Arduino IDE sketch find a string that contains "#define BOARD_TEMPLATE_ID", change "TMPL0000" by pasting Template ID from the previosu step; 
- flash the Device
The Device is ready for provision now.  

**Note: the Device will be refused by the app if it's and Product's Template ID don't match.**

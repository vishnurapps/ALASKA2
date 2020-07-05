## seeding
- we need to seed everything so that the results are reporducible
## dataframe
- two csv files are provided. 
- they are read for creating the the train df and validation df.
## Dataset class
- there is a class called Alasa dataset which crated the class
- we pass in the dataframe, test or valid data, transformation data in constructor
- based on the inputs, proper transformation is applied.
- in len, lenth of dataframe is returned
- in get_item, image is read, transformation is applied and returned.
- image is only returned for testing case.
- image and label is returned otherwise.
## Model class
- Downloads the pretrained model
- adds a new classification layer for downsizing the image size.
## Testing the working
- created a dataset based as train df
- used this dataset and obtained a data loader
- used a pretrained model to predict the output.
- Used cross entropy loss and printed the loss.
## Creating main dataset
- Used alasa dataset and created two df (need to update the size)
- We can use the prebuilt scoring mechanism.

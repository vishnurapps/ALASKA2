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
## Train function
- creates a file to save logs
- best auc score is made None
- creates train loader, validation loader, loss criterion(crossEntropyLoss), optimizer(adamw), scheduler(reduceLRonPlatue)
- two lists are made for epoch_losses and evaluation_losses
- Inside a for loop which executes for every epoch,
  - We set the model to train and set train loss to 0
  - then iterate over the contents of train_loader
    - images and labels are pushd to device
    - clear gradients
    - make predictions
    - compute loss and back propogate
    - call optimizer.step () [what it does ?](https://discuss.pytorch.org/t/how-are-optimizer-step-and-loss-backward-related/7350)
    - train loss is added to existing loss
   - train loss over epoch is calculated and added to epoch_loss
   - model is put in evaluation mode
   - evaluation loss is set to zero, two lists for actuals and predictions are made.
   - with torch.no_grad() we loop over contents of validation set.
      - images and labels are pushed to device
      - output is predicted and loss is calculated
      - in the actual list, the labels of the current loader is added.
      - in the predictions list, the predictions are also appended
      - similar to train, the loss over epoch is calculated.
    - predictions are converted to numpy array and argmax is used to select the highest value.
    - This and actual are compared to calculate the accuracy
    - there is some computations here
    - auc score is calculated using the metric function
    - the training information is added to a file
    - If the auc score is imporving, then the model is saved.
    - scheduled.step is called with new auc.
    - train loss and evaluation loss are plotted.

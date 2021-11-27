# Chubb-Assignment

In this project, there are two main functions.
- read_files(parquet_file, csv_file, xlsx_file)
- model_train(dataframe)

The read_files function is used to read three files, each in the specified format and do some pre-processing on the data such as chaging the date field format, joining data etc. and convert it into a format fit to train the model. It returns the final dataframe

The model_train function takes the final dataframe from the previous function and trains a specified model. The final model is returned which can further be used to predict on any data. It takes as input parameters a few attributes such as age of a building, number of claims made etc and predicts the claim frequency.

For this particular modelling needs, my initial intuition was to go with Ridge or linear regression. Soon, I realised that it's the wrong choice because linear regression can return negative values whereas the required output variable cannot be negative.

My next choice was the GLM family of models with gamma as the chosen family, since the output range of the variable to be predicted and the gamma distribution matched. But the results were far from satisfactory.

I next proceeded to the Poisson regression, to which I could place extra weightage on the buildings with less claims by adding a parameter sample_weights. This returned better results than the glm gamma model.

There are some points that I want to stress upon. I didn't use a ZIF model because while joining the claims with the properties dataframe, i was only able to retain the properties that had atleast one claim. (If I did a right/left join to obtain all properties, I couldn't figure how to join with the policies dataframe to obtain the term of the policy, since the start_date would be null for properties without a claim). My thought was to lookup the particular policy number from the policy dataset and fill the start_date before joining, but I couldn't join the dots.

The predictions from this model might not be the best but I can assure that I put in my best efforts in the limited time I had while managing another full-time job.
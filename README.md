## Setup

1. Create the virtual environment (for guaranteed compatibility, use python version 3.10).

    ```sh
    $ python3.10 -m venv venv
    ```

2. Enable it.

    ```sh
    $ source venv/bin/activate # if using a bash-like shell
    ```

3. Install the required libraries

    ```sh
    (venv) $ pip install -r requirements.txt
    ```

## 3.C. Timbre & Spectral Shape

For starters I didn't really have a grasp of what Timbre represents and after going back to the lecture pdfs and also doing some extensive reaserch on the internet I must confess that I still don't fully get it.. Nevertheless I have a pretty good idea now at least.

### 3.C.1. MFCCs

I begun by extracting MFCCs from each song. I didn't have to do anything fancy since there is already a librosa function which extracts mfccs from audio. I started with 13 coefficients as the task discription dictates and is the most common value if you want to get the most relevant information to the spectral envelope. I then experimented with taking the mean, median and standard deviation for each song to see what results it yields and mess around with them because I was still not sure of what would be the best feature and in what form to keep it for the recommendetion system to use as a parameter. We decided on 3 songs, 1 from each genre that we would do all our plots with so I then plotted the MFCCs heatmap for each song and then a graph of their mean, median and std deviation values for each coefficient, to visualize the differences between both the features and the songs from each genre, which would be helpful in understanding if a certain feature would be more helpful to use for the recommendation system. I then tried out the same process but with a different number of coefficients each time but I realized that the only difference was in the information added from the extra coefficients (obviously..) so I decided to just plot the above but with 20 coeffs just to get the whole picture. Since plotting the data of just 3 song didn't sum up the whole picture and also later they were not as usefull in a rough implementation of a recommendation function I wrote using only the spectral features, I wanted to check the differences of each genre regarding the mean, median and standard deviation to see if it was even worth bothering using them as features. I did that by grouping by and finding the mean of each genre for each feature. The results were pretty much the same for mean and median and a little different for std deviation but the I came to the outcome that the were not any significant differences after all.. maybe that has to do with the genres we selected and that some of the songs we selected in particular do not have such pronounced differences. Also at least for the mean and median I came to the conclusion that after 14 coeffs there was not much to seperate the 3 genres so for the final feature to be used regarding mfccs I kept the mfccs up until 14 coeffs and also added the std deviation that I had for 20 coeffs (which we ended up not using anyway). Later to try and make the MFCCs feature more pronounced and representative I added to it the 1st and 2nd derivatives to make up for a more comprehensive feature that would yield better results in the recommendation system.  

### 3.C.2. Timbre descriptors (spectral centroid, spectral bandwidth, and spectral rolloff)

For other timbre descriptors after reading the lecture slides and doing my own research I decided on extracting spectral centroid (brightness), spectral bandwidth (noise/tonal attribute) and spectral rolloff(brightness/ spectral distribution). After extracting them I decided to plot for each feature in a single plot all 3 of the selected songs to have a clear visialization of the differences a song from each genre has regarding each feature. I then added the features to the final dataframe which also contains all the above mentioned features that I saved in it to use in the recommendation system.

Then to do some tests and figure out if the features I kept are helpful and how helpful they are for a recommendation system I plotted a similarity matrix using cosine similarity (I also implemented a recommend songs function to run test and this helped me decide on which features where not really helping and then to either re-evaluate how I extract them or not use them at all and most importantly it helped in deciding which features were actually usefull). Seeing the similarity matrix we can see clearly that at least the metal songs have very similar timbral attributes, the jazz songs also kinda make for a group or 2 with similarities and finally the rock songs are not that well defined at least from the perspective of timbre only features. But we can get better results if we combine the extracted features from Harmony/Melody and Rhythm & Tempo as well.
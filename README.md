We're working on a neural network that will learn to classify music between very different genres

We used the Free Music Archive dataset - which can be found at https://github.com/mdeff/fma.
Specifically, we used the small subset of their dataset, as it was the only one with balanced genres but still had plenty of data to be used.

The notebooks in here have to be run in a specific order - each one does something to our data that other notebooks build off of.  

First, you must actually download the fma_small.zip file and the tracks.csv metadata file that are provided by the FMA
Next, after placing everything in the appropriate genres and unzipping the files, you need to run GenreSplit.  GenreSplit takes the files from an unsorted state and sorts them into their appropriate directories by genre
After this, you must run SplitAudio.  SplitAudio takes the 30 second songs provided by the FMA and turns them into 5 second snippets that our neural network uses to train.  It outputs them into a new folders.
Next, you have to run ConvertSpectrogram.  This takes all of the snippets that we have created and turns them into MelSpectrograms that are used by the neural network to train on.  It saves these into Pickle files, which can then be loaded when it is time to train the network
As the last step in training the network, you run SmallDenseNetwork.  This loads in all of the spectrogram files and then splits them into train and test sets.  It then saves a mapping for the labels used for the genres, and trains the neural network before saving the structure.
Finally, when you want to test the network, you need to get your own songs and put them into folders named "(GenreName)Test".  After creating all of these directories, you run FullSongTest.  This uses a voting system to classify full-length songs based on snippets of them that are created, and then outputs accuracies for the full length songs.

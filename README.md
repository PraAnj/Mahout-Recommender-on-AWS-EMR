# Apache Mahout example on AWS EMR cluster

This example was taken from the following AWS guide. This is a movie recommendation application based on the user ratings    
https://aws.amazon.com/blogs/big-data/building-a-recommender-with-apache-mahout-on-amazon-elastic-mapreduce-emr/    

Follow these steps,

1. Start EMR cluster with hadoop/ mahout. Use the default configurations on AWS EMR which is fine.    
2. Connect to the Master node via a SSH terminal.    
3. Get the movie rating data from following link.    

    > wget http://files.grouplens.org/datasets/movielens/ml-1m.zip    
    > unzip ml-1m.zip    

4. Convert ratings.dat to ratings.csv by running following command.

    > cat ml-1m/ratings.dat | sed 's/::/,/g' | cut -f1-3 -d, > ratings.csv    

5. Put the data (ratings.csv) into HDFS cluster.

    > hadoop fs -put ratings.csv /ratings.csv    

6. Use mahout recommenderitembased with the data on the cluster.

    > mahout recommenditembased --input /ratings.csv --output recommendations --numRecommendations 10 --outputPathForSimilarityMatrix similarity-matrix --similarityClassname SIMILARITY_COSINE

7. Use following commands to see the recommendations generated for each of the user.

    > hadoop fs -ls recommendations    
    > hadoop fs -cat recommendations/part-r-00000 | head    

8. 
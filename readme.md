#Overview 
 Download video clips and combine them back together

#Process: 
 1. Download all pieces of video from initial piece to final piece
 2. Create a combination list of all files with extension .ts 
 3. Combine all video pieces into a single video with name $output

#Future Development:
 1. Parametize extension to support other types than .ts files 
 2. Piece scope analyzer so user doesn't need to set specific start and stop pieces 

#Setup Instructions: 
 1. Get and install ffmpeg from https://www.ffmpeg.org/ you will need this to concatenate clips together into one piece
 2. You must be able to download pieces of the video you want for this code to work, check you can do that in browser
 3. You now need to get the first and last video fragment url
 	a. Open your browser's developer tools and go to network tab 
 	b. Start streaming the video and look for a .ts or .mpt or .mp2 files
	c. You will see as the video plays new fragments are downloaded in sequence 
	d. When the video first starts find the fragment number (it is almost always 0 or 1 with some set of leading zeroes)
 		i. ex. For  start fragment http://test.com/movie_0001 the first fragment is 1 (do not write leading zeroes)
 	d. Go to end of the video and you will see the HIGHEST fragment number (write this number down)
		i. ex. For end fragment http://test.com/movie_1000 the highest fragment is 1000
 	e. You now also know the URL prefix the video pieces have (write this prefix down)
		i. ex. For fragment http://test.com/movie_1000.ts the prefix is http://test.com/movie_ (no 1000)
 4. Get the CURL command to download the video fragment 
	a. Right click on the video fragment in your network tab and click "copy->copy as curl"
 	b. Replace the "XYZ" portions of the curl command with your REAL values   
 5. Pick a name for your output folder and video
	a. ex if you are downloading http://test.com/movie_1000.ts you might want to name your output movie
 6. You can now construct your download command 

#To Download 1 video:
 1. From the root directory where download.sh is located run the following command (no quotes): 
 "sh download.sh https://website.domain/video_prefix_ 1 999999999999 OUTPUT_NAME_NO_EXTENSION" 

#To Download multiple videos (from same site):
 1. Edit batch.sh adding one line for each video
 2. From the root directory where download.sh is located run the following command (no quotes):
 "sh batch.sh"
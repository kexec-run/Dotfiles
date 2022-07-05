

# Add audio to an image
```
ffmpeg -loop 1 -i IMG_3090.JPG -i MEGALOBOX.mp3 -c:v libx264 -tune stillimage -c:a aac -b:a 192k -vf "scale='iw-mod(iw,2)':'ih-mod(ih,2)',format=yuv420p" -shortest -movflags +faststart out.mp4ffmpeg -loop 1 -i IMG_3090.JPG -i MEGALOBOX.mp3 -c:v libx264 -tune stillimage -c:a aac -b:a 192k -vf "scale='iw-mod(iw,2)':'ih-mod(ih,2)',format=yuv420p" -shortest -movflags +faststart output.mp4
```

-------------------------

# Video stabilization

```

Install ffmpeg and libvidstab


# The first pass ('detect') generates stabilization data and saves to `transforms.trf`
# The `-f null -` tells ffmpeg there's no output video file
ffmpeg -i clip.mkv -vf vidstabdetect -f null -

# The second pass ('transform') uses the .trf and creates the new stabilized video.
ffmpeg -i clip.mkv -vf vidstabtransform clip-stabilized.mkv
```

[Source](https://www.paulirish.com/2021/video-stabilization-with-ffmpeg-and-vidstab/)

---------------------------------------


# Downloading YouTube videos as audio with yt-dlp

```
yt-dlp -f 'ba' https://www.youtube.com/watch?v=dQw4w9WgXcQ -o '%(id)s.%(ext)s'
```

[Source](https://write.corbpie.com/downloading-youtube-videos-as-audio-with-yt-dlp/)

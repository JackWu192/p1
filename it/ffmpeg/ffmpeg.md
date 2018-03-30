# Learning Note of ffmpeg.
Source [ffmpeg documentation](https://ffmpeg.org/documentation.html)
ffmpeg actually is a suit of tools and libraries for working with media files. 

## Four command line tools
	ffmpeg : main tool 
	ffprobe: analysing tool
	ffplay : player
	ffserver: a media server
Each tool has two documents, the simple version and the "xxx-all" version.

## Components 
ffmpeg tools calls components API to do the job. On most of time, command line tool passes proper arguments to 
functions of these components based on tasks. For complicate tasks, user can transfer arguments to these components
directly. 

Following are components that has documents on the website
	Utilities
	Video scaling and pixel format converter
	Audio re-sampler
	Encoders and decoders (codecs)
	Bitstream filters
	Muxers and demuxers (formats)
	Protocols
	Input and output devices
	Filters

## Libraries 
Libraries are used by both tools and components. Ffmpeg documented following libraries
	libavutil
	libswscale
	libswresample
	libavcodec
	libavformat
	libavdevice
	libavfilter

## API 
Other than above user level documentation, ffmpeg also documented API for developers. These are in Doxygen format based on versions.

## Others
Among these useful documents officially provided by ffmpeg, there are General Documents that provide FAQ, External lib supporting misc and 
Community Contributed Documentation and a book.


This memory note will focus on Tools, Component and Library documents. 


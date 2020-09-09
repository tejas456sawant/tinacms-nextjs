---
author: Tejas Sawant
date: 'Tue Sep 08 2020 14:11:32 GMT+0530 (India Standard Time)'
title: Course
---
**Demo** :- [**https://youtubethumbnaildownloader.geeksfortech.com**](https://youtubethumbnaildownloader.geeksfortech.com "https://youtubethumbnaildownloader.geeksfortech.com")

Following article shows how you can create youtube thumbnail downloader. For this project we are going to use Nextjs and tailwind css. First we are going to create nextjs with tailwind css. You can use following command.

    npx create-next-app --example with-tailwindcss youtube-thumbnail-downloader

[**![Create Project](https://geeksfortech.com/static/100892f2956628f950ef7738681053bb/fcda8/create-project.png "Create Project")**](https://geeksfortech.com/static/100892f2956628f950ef7738681053bb/160a3/create-project.png)

This command will create next app with tailwind css.

1. Creating **Input** for accepting youtube url.

    <form className="w-full max-w-md">
      <div className="flex items-center border-b border-teal-500 py-2">
        <input
          className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          placeholder="Enter Youtube URL"
        />
        <button
          className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
          type="button"
        >
          Download
        </button>
      </div>
    </form>

[**![Input Box](https://geeksfortech.com/static/e2076ad56ddf863f6a56e192dfc63580/79e1b/input-box.png "Input Box")**](https://geeksfortech.com/static/e2076ad56ddf863f6a56e192dfc63580/79e1b/input-box.png)

2. Then creating function for checking whether entered url is correct youtube url or not.

    const getYouTubeThumbnail = url => {
      //regex for matching youtube url
      let regExp = /.*(?:youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=)([^#\&\?]*).*/
      let match = url.match(regExp)
      if (match && match[1].length == 11) {
        let videoURL = match[1]
        //videoURL is holding video url like aabbssccddffj it is 11 letters url.
      } else {
        console.log(
          "The URL you have entered maybe incorrect. Please Enter a correct URL."
        )
      }
    }

3. Now we are going to create state for our thumbnail urls, actual video url entered by user and for error.

    //imporing useState from react
    import { useState } from "react"
    
    // functional component
    const Index = () => {
      const [error, seterror] = useState("")
      const [videoURL, setVideoURL] = useState("")
      const [HDImage_1280_720, setHDImage_1280_720] = useState("")
      const [SDImage_640_480, setSDImage_640_480] = useState("")
      const [NormalImage_480_360, setNormalImage_480_360] = useState("")
      const [NormalImage_320_180, setNormalImage_320_180] = useState("")
      const [NormalImage_120_90, setNormalImage_120_90] = useState("")
    }

4. Next storing enterd url in state also creating text field using **span** for conditional rendering of errors.

    ;<form className="w-full max-w-md">
      <div className="flex items-center border-b border-teal-500 py-2">
        <input
          className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          value={videoURL}
          placeholder="Enter Youtube URL"
          onChange={event => {
            setVideoURL(event.target.value)
            console.log(event.target.value)
          }}
        />
        <button
          className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
          type="button"
        >
          Download
        </button>
      </div>
    </form>
    {
      error && <span className="font-black">{error}</span>
    }

5. Completing **getYouTubeThumbnail()** function and updating with videos urls states.

    const getYouTubeThumbnail = url => {
      let regExp = /.*(?:youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=)([^#\&\?]*).*/
      let match = url.match(regExp)
      if (match && match[1].length == 11) {
        let videoURL = match[1]
        setHDImage_1280_720(
          "http://img.youtube.com/vi/" + videoURL + "/maxresdefault.jpg"
        )
        setSDImage_640_480(
          "http://img.youtube.com/vi/" + videoURL + "/sddefault.jpg"
        )
        setNormalImage_480_360(
          "http://img.youtube.com/vi/" + videoURL + "/hqdefault.jpg"
        )
        setNormalImage_320_180(
          "http://img.youtube.com/vi/" + videoURL + "/mqdefault.jpg"
        )
        setNormalImage_120_90(
          "http://img.youtube.com/vi/" + videoURL + "/default.jpg"
        )
        seterror("")
      } else {
        seterror(
          "The URL you have entered maybe incorrect. Please Enter a correct URL."
        )
      }
    }

6. Passing values to **getYouTubeThumbnail()** function and adding image tags with there **src** as states.

    const index = () => {
      return (
        <div>
          //Text Input Field Code
          <button
            className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
            type="button"
            onClick={() => {
              getYouTubeThumbnail(videoURL)
            }}
          >
            Download
          </button>
          // Repeat code for SDImage_640_480, NormalImage_480_360
          //NormalImage_320_180, NormalImage_120_90
          <img
            src={HDImage_1280_720}
            alt="HDImage_1280_720"
            className="mb-3 object-center"
          />
        </div>
      )
    }
    export default Index

[**![Input Box](https://geeksfortech.com/static/db3510db653747abf58b44838a09f6ab/63868/button.png "Button")**](https://geeksfortech.com/static/db3510db653747abf58b44838a09f6ab/63868/button.png)

7. At last going to add button for downloading thumbnail and then redirecting to thumbnail url.

    // Repeat code for SDImage_640_480, NormalImage_480_360
    // NormalImage_320_180, NormalImage_120_90
    <button className="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mb-5 inline-flex">
      <svg
        className="fill-current w-4 h-4 mr-2 mt-1"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
      >
        <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
      </svg>
      <a href={HDImage_1280_720} target="_blank">
        HD Image (1280x720)
      </a>
    </button>

Final Code looks like following.

    import { useState } from "react"
    
    const Index = () => {
      const [error, seterror] = useState("")
      const [videoURL, setVideoURL] = useState("")
      const [HDImage_1280_720, setHDImage_1280_720] = useState("")
      const [SDImage_640_480, setSDImage_640_480] = useState("")
      const [NormalImage_480_360, setNormalImage_480_360] = useState("")
      const [NormalImage_320_180, setNormalImage_320_180] = useState("")
      const [NormalImage_120_90, setNormalImage_120_90] = useState("")
    
      const getYouTubeThumbnail = url => {
        let regExp = /.*(?:youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=)([^#\&\?]*).*/
        let match = url.match(regExp)
        if (match && match[1].length == 11) {
          let videoURL = match[1]
          setHDImage_1280_720(
            "http://img.youtube.com/vi/" + videoURL + "/maxresdefault.jpg"
          )
          setSDImage_640_480(
            "http://img.youtube.com/vi/" + videoURL + "/sddefault.jpg"
          )
          setNormalImage_480_360(
            "http://img.youtube.com/vi/" + videoURL + "/hqdefault.jpg"
          )
          setNormalImage_320_180(
            "http://img.youtube.com/vi/" + videoURL + "/mqdefault.jpg"
          )
          setNormalImage_120_90(
            "http://img.youtube.com/vi/" + videoURL + "/default.jpg"
          )
          seterror("")
        } else {
          seterror(
            "The URL you have entered maybe incorrect. Please Enter a correct URL."
          )
        }
      }
    
      return (
        <div className="mt-15 md:mt-10 lg:mt-10 mx-auto">
          <center>
            <form className="w-full max-w-md">
              <div className="flex items-center border-b border-teal-500 py-2">
                <input
                  className="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
                  type="text"
                  value={videoURL}
                  placeholder="Enter Youtube URL"
                  onChange={event => {
                    setVideoURL(event.target.value)
                    console.log(event.target.value)
                  }}
                />
                <button
                  className="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
                  type="button"
                  onClick={() => {
                    getYouTubeThumbnail(videoURL)
                  }}
                >
                  Download
                </button>
              </div>
            </form>
            {error && <span className="font-black">{error}</span>}
            {!error && HDImage_1280_720 !== "" ? (
              <div className="mt-10">
                <button className="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mb-5 inline-flex">
                  <svg
                    className="fill-current w-4 h-4 mr-2 mt-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <a href={HDImage_1280_720} target="_blank">
                    HD Image (1280x720)
                  </a>
                </button>
                <img
                  src={HDImage_1280_720}
                  alt="HDImage_1280_720"
                  className="mb-3 object-center"
                />
                <button className="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mb-5 inline-flex">
                  <svg
                    className="fill-current w-4 h-4 mr-2 mt-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <a href={SDImage_640_480} target="_blank">
                    SD Image (640x480)
                  </a>
                </button>
                <img
                  src={SDImage_640_480}
                  alt="HDImage_1280_720"
                  className="mb-3 object-center"
                />
                <button className="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mb-5 inline-flex">
                  <svg
                    className="fill-current w-4 h-4 mr-2 mt-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <a href={NormalImage_480_360} target="_blank">
                    Normal Image (480x360)
                  </a>
                </button>
                <img
                  src={NormalImage_480_360}
                  alt="HDImage_1280_720"
                  className="mb-3 object-center"
                />
                <button className="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mb-5 inline-flex">
                  <svg
                    className="fill-current w-4 h-4 mr-2 mt-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <a href={NormalImage_320_180} target="_blank">
                    Normal Image (320x180)
                  </a>
                </button>
                <img
                  src={NormalImage_320_180}
                  alt="HDImage_1280_720"
                  className="mb-3 object-center"
                />
                <button className="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mb-5 inline-flex">
                  <svg
                    className="fill-current w-4 h-4 mr-2 mt-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path d="M13 8V2H7v6H2l8 8 8-8h-5zM0 18h20v2H0v-2z" />
                  </svg>
                  <a href={NormalImage_120_90} target="_blank">
                    Normal Image (120x90)
                  </a>
                </button>
                <img
                  src={NormalImage_120_90}
                  alt="HDImage_1280_720"
                  className="mb-3 object-center"
                />
              </div>
            ) : (
              ""
            )}
          </center>
        </div>
      )
    }
    export default Index
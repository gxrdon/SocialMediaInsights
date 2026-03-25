# Social Media Insights
This project serves as a POC for aggregating social media analytics across all major platforms (Instagram, TikTok, YouTube) into a centralized cloud platform (AWS) to drive insights.

## Infra
The infrastructure is defined using Infrastructure as Code tooling (CDK) to safely deploy changes and maintain state.

## Lambdas 
The core processing behind the workflows that pull analytics is AWS Lambda. Each social media platform will have it's own Lambda function responsible for retrieving the most recent analytics from the respective platform and uploading them to the data lake. The northstar is Iceberg but for now, as this is a POC, we will store raw data and iterate from there.

### EventBridge
In order to run the Lambdas on a set cadence, we will use EventBridge to schedule these jobs every 24 hours. Depending on the specific user's needs, we can configure this value to grant more granular metrics.

# Cross-Posting
Most creators maintain multiple social media platforms and must manually upload their videos to each of these platforms. On top of the aforemention analytics platform I proposed, I'd like to create another workflow that automates this process. I envision that video can be uploaded to an S3 "ready to post" bucket, where new objects in the bucket trigger a Lambda that is responsible for uploading these videos to all specified platforms as a draft or unlisted video. From there, it can transcribe the video and come up with a title and description and upload, if permitted.

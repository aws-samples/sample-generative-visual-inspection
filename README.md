## Zero-Training Visual Defect Detection Using Amazon Nova Pro

In manufacturing, visual quality inspection is critical for ensuring product reliability<br/>
and compliance. However, traditional approaches—whether manual review or custom-trained<br/>
computer vision models—are costly, slow to adapt, and difficult to scale across diverse<br/>
product lines.

This Jupyter notebook introduces a zero-training, no-dataset-required visual inspection<br/>
system using **Amazon Nova Pro**, a multimodal foundation model accessed via **Amazon Bedrock**.<br/>
Using only a **Jupyter notebook**, you can detect manufacturing defects in product images with structured<br/>
natural language prompts—no computer vision expertise or labeled data required.<br/>
By the end of this notebook, you'll be able to:

* Upload and analyze product images in a Jupyter notebook
* Detect visual defects using Amazon Nova Pro
* Automatically return bounding boxes, failure reasons, and QC status
* Visualize defect overlays on product images

For more background consult the Readme in the same repository.

## Pipeline Architecture in this Notebook

This inspection pipeline operates entirely within a local Jupyter notebook and AWS Generative AI infrastructure:

1. Image Capture: Use widgets in the notebook to upload a product image (and optionally a reference image).
2. Image Preprocessing: Images are resized, converted to Base64, and prepared for inference.
3. Generative AI Inference: Amazon Bedrock invokes Nova Pro to analyze the image and return structured defect data.
4. Visualization: Bounding boxes and defect reasons are drawn using matplotlib.

User → Jupyter Notebook → Amazon Bedrock (Nova Pro) → JSON Defect Output → Matplotlib Overlay

### Getting Started

There is a Cloudformation template available that will create an Amazon Sagemaker Ai Notebook and clones this repository.
The output of the Cloudformation is a URl to open the Notebook.

Run [this Cloudformation link](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://ws-assets-prod-iad-r-iad-ed304a55c2ca1aee.s3.us-east-1.amazonaws.com/02f82da5-d6b0-403b-9619-7bb8e506a21a/Notebook-Cloudformation.yaml&stackName=VisualInspectionwithGenerativeAI) and then open the link in the outputs.

### Permissions

If you manually run the notebook on an EC2 instance or your own laptop
ensure the credentials you have can invoke the Amazon Nova models. 

And also ensure you have granted access through the AWS Console: <br/>
Bedrock → Model Access → Modify model access

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": "bedrock:InvokeModel",
			"Resource": "*"
		}
	]
}
```

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.


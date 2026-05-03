# infra
name: Create s3 Static Site

on:
  issues: 
    type:
      - opened

jobs:
    deploy:
      runs-on: ubuntu-latest
      steps:
      - name: Checkout Repository 
        uses: actions/checkout@v2

      - name: Set up AWS CLI
        uses: aws-actions/configure-aws-credentials@v2

        with:    
        aws-access-key-id: ${{secrets.AWS-ACCESS_KEY_ID}}
        aws-secret-access-key: #{{secrets.AWS_SECRET_ACCESS_KEY}}
        aws-region:us-east-1 # substutua pela reion desejada

      - name: Extract Bucket Name from Issue
        run:
          export BUCKET_NAME=|$echo "${{ github.event.issue.title }}")
          echo Bucket Name: $BUCKET_NAME"
          echo "BUCKET_NAME= $BUCKET_NAME"  >> $GITHUB_ENV

      -name: Run Terraform
      run
        cd trrraform
        cd s3-bucket-static
        terraform innit
        terraform apply -auto-approve -var="bucket_name=${{ env.BUCKET
        
      -name: Add comment
      
      run: gh issue coment "$NUMBER" --repo "$REPO"  body "$BODY"
      env:
      GITHUB_TOKEN: ${{ secrets.GH_TOKEN}}
      NUMBER: ${{ github-event.issue.number}}
      REPO: >
        O bucket S3 foi criado com sucesso!


       

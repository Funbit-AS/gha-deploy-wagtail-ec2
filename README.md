# deploy-wagtail-ec2
This action will deploy a single container Wagtail project to an AWS EC2 instance. 

## Usage
The custom action will take the following inputs:
- `project-name `: name of the project
- `deployment-target `: either `staging` or `production`
- `image-name `: name of the image that we will build
- `service-name `: name of the service/container as defined in the infrastucture docker-compose file.
- `aws-access-key-id `: Should be given using secrects
- `aws-secret-access-key `: Should be given using secrects
- `aws-region `:
- `uses-tailwind `: Optional. should be `false` (case sensitive) if the project does not use tailwind. Anything else will be interpreted as true.
- `elm-paths `: Optional. All paths to elm files ( /wagtail/{{ project-name }}/{{ folder }}/elm ) in project seperated by whitespace
- `elm-version `: Optional. Version number of elm.

## Example Usage



    steps:
      - name: Checkout
        uses: actions/checkout@v3
      
      - name: Custom Deploy Action
        uses: Funbit-AS/gha-deploy-wagtail-ec2@v1
        with:
          project-name: funbitno
          deployment-target: staging
          image-name: web
          service-name: web
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}
          uses-tailwind: True
          elm-paths: /wagtail/funbitno/projects/elm
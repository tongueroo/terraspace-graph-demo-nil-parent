# Terraspace Demo Graph for Debugging

To debug this

https://community.boltops.com/t/plan-stack-trace-error-after-making-change-to-existing-infra/828

## Graphs

To draw the full dependency graph defined by this project's resources:

    terraspace all graph

Produces this:

![](https://img.boltops.com/boltops/repos/terraspace-graph-demo/full-graph.png)

## Debugging

Used the `config.all.include_stacks` option in

[config/app.rb](config/app.rb)

```ruby
Terraspace.configure do |config|
  config.all.include_stacks = ["b1"]
end
```

Still able to deploy one of the stacks. Example:

$ terraspace up c1
Building .terraspace-cache/us-west-2/dev/stacks/c1
Downloading tfstate files for dependencies defined in tfvars...
Built in .terraspace-cache/us-west-2/dev/stacks/c1
=> terraform apply -input=false

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:
  # random_pet.this will be created
  + resource "random_pet" "this" {
      + id        = (known after apply)
      + length    = 2
      + separator = "-"
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + length = 2
  + pet    = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes
random_pet.this: Creating...
random_pet.this: Creation complete after 0s [id=smooth-magpie]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

length = 2
pet = "smooth-magpie"
Time took: 2s
$


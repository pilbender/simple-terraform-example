variable "access_key" {}
variable "secret_key" {}
variable "keypair_name" {}
variable "region" {
  default = "us-east-1"
}
variable "ssh_private_key" {}

provider "aws" {
  access_key = "${var.access_key}"
  secret_key = "${var.secret_key}"
  region     = "${var.region}"
}

resource "aws_instance" "scott-terraform" {
  # Ubuntu 16.04 LTS Server
  ami           = "ami-24144f5e"
  instance_type = "t2.micro"
  tags {
    Name = "scott-terraform"
  }

  key_name = "${var.keypair_name}"

  provisioner "local-exec" {
    command = "sleep 120; ssh -o 'StrictHostKeyChecking no' -i ${var.ssh_private_key} ubuntu@${aws_instance.scott-terraform.public_ip} 'sudo ln -s /usr/bin/python3 /usr/bin/python'; ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -u ubuntu --private-key ~/downloads/kubernetes/scott-smith.pem -i '${aws_instance.scott-terraform.public_ip},' -i inventories/home/hosts ../ansible/site.yml"
  }
}

output "ip" {
  value = "${aws_instance.scott-terraform.public_ip}"
}

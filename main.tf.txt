resource "aws_instance" "appec2" {



  ami                    = "ami-0d81306eddc614a45"
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.appsg.id]



  key_name  = "tf-key-pair"
  subnet_id = var.subnet_id
  tags = {
    Name = "app"
  }
}

resource "aws_security_group" "appsg" {
  name   = "app-sg"
  vpc_id = var.vpc_id



  ingress {
    from_port   = 9000
 to_port     = 9000
    protocol    = "tcp"
    cidr_blocks = ["10.0.0.0/20"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

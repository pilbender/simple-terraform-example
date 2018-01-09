provider "kubernetes" {
  host = "192.168.99.100"
}

resource "kubernetes_pod" "nginx" {
  metadata {
    name = "scott-terraform"
    labels {
      App = "nginx"
    }
  }

  spec {
    container {
      image = "nginx:1.7.8"
      name = "example"
      port {
        container_port = 80
      }
    }
  }
}

resource "kubernetes_service" "nginx" {
  metadata {
    name = "scott-terraform"
  }
  spec {
    selector {
      App = "nginx"
    }
    port {
      port = 80
      target_port = 80
    }

    type = "LoadBalancer"
  }
}

output "lb_ip" {
  value = "192.168.99.100"
}


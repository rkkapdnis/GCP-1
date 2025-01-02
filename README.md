export GOOGLE_APPLICATION_CREDENTIALS="/path/to/your/service-account-file.json"

# main.tf

provider "google" {
  project = "<your-gcp-project-id>"
  region  = "us-central1"
  zone    = "us-central1-a"
}

# Create the Ubuntu VM instance
resource "google_compute_instance" "ubuntu_vm" {
  name         = "ubuntu-vm"
  machine_type = "e2-medium"   # Choose machine type as per your requirement
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "ubuntu-2004-focal-v20211105"  # Ubuntu 20.04 LTS image
    }
  }

  network_interface {
    network = "default"
    access_config {
      # Use NAT for internet access
    }
  }

  tags = ["web"]
}


#access VM
gcloud compute ssh ubuntu-vm --zone=us-central1-a

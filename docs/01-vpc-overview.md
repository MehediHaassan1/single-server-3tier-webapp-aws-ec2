# VPC Setup

## What I did

I created a custom VPC for this project.

## Configuration

- VPC Name: single-server-vpc
- CIDR: 10.0.0.0/16

## Why I did this

I needed an isolated network to host my 3-tier application securely.

## Result

This VPC acts as the base network for all AWS resources like EC2, subnets, and routing.

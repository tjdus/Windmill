# Windmill

Four blades revolve around the windmill.
Assets are attached

## Source Code


  import pygame
  import os
  import numpy as np

  WINDOW_WIDTH = 800
  WINDOW_HEIGHT = 600

  GRAY = (200, 200, 200)
  BLACK = (0,0,0)
  WHITE = (255,255,255)

  CenterPos= WINDOW_WIDTH / 2 , WINDOW_HEIGHT /2

  pygame.init()

  pygame.display.set_caption("Windmill")

  screen = pygame.display.set_mode((WINDOW_WIDTH, WINDOW_HEIGHT))

  clock = pygame.time.Clock()

  current_path = os.path.dirname(__file__)
  assets_path = os.path.join(current_path, 'assets')

  Windmillimg= pygame.image.load(os.path.join(assets_path, 'windmill.png'))
  Bladeimg= pygame.image.load(os.path.join(assets_path, 'blade.png'))



Initialize pygame. And upload images.

  class Blade(pygame.sprite.Sprite):
    def __init__(self, image, center, degree):
        pygame.sprite.Sprite.__init__(self)
        self.base=image
        self.image= self.base
        w,h= self.image.get_size()
        self.position = pygame.Vector2(center)
        self.rot=0
        self.rot_speed = 1        
        self.offset = pygame.Vector2(-w//2+20,0)
        self.offset_rotated = (0,0)
        self.degree = degree
      
    def rotate(self):     
        self.image = pygame.transform.rotozoom(self.base, -self.rot-self.degree, 1)
        self.offset_rotated = self.offset.rotate(self.rot+self.degree)
        self.rect = self.image.get_rect(center = self.position - self.offset_rotated)
        
    def update(self):
        self.rot += self.rot_speed
        self.rotate()
        
Rotate the image based on the original image. And offset the changes by the rotation around the central axis.

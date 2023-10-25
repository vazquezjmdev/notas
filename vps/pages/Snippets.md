- #+BEGIN_EXAMPLE
  #avoid iframes
  add_header X-Frame-options SAMEORIGIN;
  
  #avoid mime
  add_header X-Content-Type-Options nosniff;
  
  #avoid XSS
  
  add_header X-XSS-Protection "1; mode=block";
  
  # Refferrer policy
  add_header Referrer-Policy "strict-origin-when-cross-origin";
  #+END_EXAMPLE
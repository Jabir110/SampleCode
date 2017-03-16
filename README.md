<h2>App Transport Securit</h2>

     <key>NSAppTransportSecurity</key>

        <dict>

           <key>NSAllowsArbitraryLoads</key>

           <true/>

        </dict>

<h2>NSUserDefault</h2>

      NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                     
      [defaults setObject:[@"Jabir" forKey:@"strVanue"];
                     
      [defaults synchronize];
                      
      NSLog(@"strVanue : %@",[defaults valueForKey:@"strVanue"]);

<h2>AlertView</h2>

     //Declare
     
     UIAlertView *alert =  [[UIAlertView alloc]initWithTitle:@"Title" message:@"Message" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil];
     alert.tag = 101;
     [alert show];
     
     //Index Method
     
     - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex
     {
          if (alertView.tag == 101)
          {
               if (buttonIndex == 0)
               {
                    txtConfirmPass.text = @"";
                    txtNewPass.text = @"";
                    txtCurrentPass.text = @"";
               }
          }
     }
     
<h2>TextField Validation</h2>



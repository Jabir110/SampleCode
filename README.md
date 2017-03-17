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
     
     NSString *emailRegEx = @"[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}";
     NSPredicate *emailTest = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegEx];
    
     if(txtMobile.text.length == 0)
     {
          [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter Name" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
     }
     else if(txtMobile.text.length < 10)
     {
          [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter valid Phone Number" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
     }
     else if(txtMobile.text.length > 10)
     {
          [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter valid Phone Number" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
     }
     else if(txtEmail.text.length == 0)
     {
          [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter Email" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
     }
     else if([emailTest evaluateWithObject:txtEmail.text] == NO)
     {
          [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter valid Email" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
     }
  
<h2>Push & Pop With StoryBoardID</h2>

     //Push
     BuyMembershipViewController *push=[self.storyboard instantiateViewControllerWithIdentifier:@"BuyMembershipViewController"];
     [self.navigationController pushViewController:push animated:YES];
     
     //Pop
     [self.navigationController popViewControllerAnimated:YES];

<h2>Push With Segue</h2>

     - (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
     {
          if ([[segue identifier] isEqualToString:@"MySegue"])
          {
               // Get destination view
               SecondViewController *vc = [segue destinationViewController];
               vc.strPass = [NSString stringWithFormat:@"Jabir"];
          }
     }
     
     - (IBAction)ActionButton:(id)sender
     {
          [self performSegueWithIdentifier:@"MySegue" sender:sender];
     }
     
     

     
     


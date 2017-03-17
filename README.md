<h2>App Transport Securit</h2>

     <key>NSAppTransportSecurity</key>
        <dict>
           <key>NSAllowsArbitraryLoads</key>
           <true/>
        </dict>

<h2>NSUserDefault</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController
     
     - (void)viewDidLoad
     {
          [super viewDidLoad];
    
          NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
          [defaults setObject:@"Jabir" forKey:@"strVanue"];
          [defaults synchronize];
     }


<h2>AlertView</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController
     
     - (void)viewDidLoad 
     {     
          UIAlertView *alert =  [[UIAlertView alloc]initWithTitle:@"Title" message:@"Message" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil];
          alert.tag = 101;
          [alert show];
     }
     
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
    
<h2>Push With Segue (tableView)</h2>

          -(void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
          {
               if ([segue.identifier isEqualToString:@"pushSecond"]) 
               {
                    NSIndexPath *indexpath=[tblView indexPathForSelectedRow];
                    secondVc *ViewSecond=segue.destinationViewController;
                    ViewSecond.strData=[NSString stringWithFormat:@"%@",[arr objectAtIndex:indexpath.row]];
               }
          }
     
     -(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
     {
          [self performSegueWithIdentifier:@"pushSecond" sender:nil];
     }
     
<h2>pop & Back Button DataPass (StoryBoardID)</h2>
     
   We can use a delegate to pass the data back to previous Controller.So if You are in your NextViewController and you need to pass the data to VieController than you need to create a protocol that sends data back to your ViewController.Your ViewController  would become a delegate of NextViewController.

Steps:

1. Create a new Xcode Project for (Single View Application).
2. Give Project a name ( Lets say ProtocolDemo).
3. Click next button and the Project will be created.
4. Now go to Your StoryBoard , Click on the View Controller. Then Click on the Xcode options”Editor” and then embed a navigation Controller.  Take a label and a button on the ViewController and make proper connections. Your ViewController.h and ViewController.m will look something like this

          #import <UIKit/UIKit.h>
          @interface ViewController : UIViewController
          @property (weak, nonatomic) IBOutlet UILabel *outputLabel;
          @end

          -(void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
          {
               if ([segue.identifier isEqualToString:@"pushSecond"]) 
               {
                    NSIndexPath *indexpath=[tblView indexPathForSelectedRow];
                    secondVc *ViewSecond=segue.destinationViewController;
                    ViewSecond.strData=[NSString stringWithFormat:@"%@",[arr objectAtIndex:indexpath.row]];
               }
          }

     

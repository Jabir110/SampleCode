<h2>App Transport Securit</h2>

```objective-c
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
    
```
<h2>NSUserDefault</h2>

```objc
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
[defaults setObject:@"Jabir" forKey:@"strVanue"];
[defaults synchronize];
```

<h2>AlertView</h2>

```objc
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
```

<h2>TextField Validation</h2>

```objc
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
```

<h2>Push & Pop With StoryBoardID</h2>

```objc
- (IBAction)ActionPushButton:(id)sender
{
    SecondViewController *push=[self.storyboard instantiateViewControllerWithIdentifier:@"SecondViewController"];
    [self.navigationController pushViewController:push animated:YES];
}    

- (IBAction)ActionBackButton:(id)sender
{
    [self.navigationController popViewControllerAnimated:YES];
}
```

<h2>Push With Segue</h2>

```objc
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
```

<h2>Push With Segue (tableView)</h2>

```objc
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
```

<h2>Pop & Back Button DataPass (StoryBoardID)</h2>

[Example](https://iostpoint.wordpress.com/2016/06/25/pass-data-back-to-previous-viewcontroller/)

ViewController.h

```objc
#import <UIKit/UIKit.h>

@interface ViewController : UIViewController
@property (weak, nonatomic) IBOutlet UILabel *outputLabel;
- (IBAction)ActionNext:(id)sender;

@end
```

ViewController.m

```objc
#import "ViewController.h"
#import "SecondViewController.h"

@interface ViewController ()
@end

@implementation ViewController

- (IBAction)ActionNext:(id)sender
{
    SecondViewController *acontollerobject=[self.storyboard instantiateViewControllerWithIdentifier:@"SecondViewController"];
    acontollerobject.delegate=self; // protocol listener
    [self.navigationController pushViewController:acontollerobject animated:YES];
}    
-(void)sendDataToPreviousController: (NSString *)string
{
    NSLog(@"Fired");
    self.outputLabel.text = string;
}
```

SecondViewController.h

```objc
#import <UIKit/UIKit.h>

@protocol sendDataBack <NSObject>
-(void)sendDataToPreviousController: (NSString *)string;

@end

@interface SecondViewController : UIViewController
@property (assign,nonatomic) id delegate;

@end
```
     
SecondViewController.m

```objc
#import "SecondViewController.h"

@interface SecondViewController ()<UITextFieldDelegate>
@property (weak, nonatomic) IBOutlet UITextField *inputTextField;
     
@end

@implementation SecondViewController

-(void)textFieldDidEndEditing:(UITextField *)textField
{
    [_delegate sendDataToPreviousController:textField.text];
}
```

<h2>CollectionView Width SET</h2>

```objc
- (CGSize)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath *)indexPath
{
    CGSize returnSize = CGSizeZero;
    
    float cellWidth = self.view.frame.size.width/2-15;
    // float cellhight=self.view.frame.size.width/2-37;
    float cellhight=205.0f;
    
    NSLog(@"cellhight :%f",cellhight);
    NSLog(@"cellWidth :%f",cellWidth);
    
    returnSize = CGSizeMake(cellWidth, cellhight);
        
    return returnSize;
}
```

<h2>Date Formetter</h2>

```objc
NSDate *date = [NSDate date];
NSLog(@"date: %@",date);

NSDateFormatter* dateFormatter = [[NSDateFormatter alloc] init];
[dateFormatter setTimeZone:[NSTimeZone timeZoneWithName:@"GMT"]];
[dateFormatter setDateFormat:@"dd/MM/yyyy"];

//Convert Date to String
NSString *strDate = [dateFormatter stringFromDate:date];
NSLog(@"strDate: %@",strDate);

//Convert String to Date
NSDate *ConvertDate = [dateFormatter dateFromString:strDate];
NSLog(@"ConvertDate: %@",ConvertDate);
```

<h2>Date Get</h2>

Only Get EndDate

```objc
NSDate *StartDate = [NSDate date];

NSDateComponents *dateComponents = [[NSDateComponents alloc] init];
[dateComponents setDay:15];

NSDate *EndDate = [[NSCalendar currentCalendar] dateByAddingComponents:dateComponents toDate:StartDate options:0];

NSLog(@"StartDate: %@",StartDate);
NSLog(@"EndDate: %@",EndDate);
```

List of All date between Two Dates

```objc

NSMutableArray *result = [NSMutableArray array];
NSDate *StartDate = [NSDate date];
NSCalendar *cal = [NSCalendar currentCalendar];

NSDateComponents *comps = [cal components:(NSCalendarUnitYear | NSCalendarUnitMonth | NSCalendarUnitDay)fromDate:StartDate];

NSDate *date = [cal dateFromComponents:comps];
NSLog(@"date: %@",date);

NSDateFormatter* dateFormatter = [[NSDateFormatter alloc] init];
[dateFormatter setDateFormat:@"dd/MM/yyyy"];

for (int i = 0 ; i < 15; i ++)
{
    NSString *strDate = [dateFormatter stringFromDate:date];    
    [result addObject:strDate];
    [comps setDay:(comps.day + 1)];
    date = [cal dateFromComponents:comps];
}
NSLog(@"Result: %@",result);
```

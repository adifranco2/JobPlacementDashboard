# Live Project

## Introduction

During a two-week time period, I worked with other students at The Tech Academy to continue development of a full scale MVC Web Application in C#.  During the sprint I had the opportunity to complete several back-end stories. 

Below are descriptions of the stories I worked on and related code snippets.

### Adding Classes to Table-Per-Hierarchy Table

The model required two new classes that inherited from the existing class.  My task was to create the new classes while ensuring that a TPH table was generated in the database.

```
public class RentalEquiptment : Rental
{
  [Display(Name = "Chocking Hazard")]
  public bool ChokingHazard { get; set; }
  [Display(Name = "Suffocation Hazard")]
  public bool SuffocationHazard { get; set; }
  [Display(Name = "Purchase Price")]
  public int PurchasePrice { get; set; }
}

public class RentalRoom : Rental
{
  [Display(Name = "Room Number")]
  public int RoomNumber { get; set; }
  [Display(Name = "Square Footage")]
  public int SquareFootage { get; set; }
  [Display(Name = "Maximun Occupancy")]
  public int MaxOccupancy { get; set; }
}  
  ```
  
### Seeding Database Table

I was tasked with seeding a database table with objects that may or may not be associated with objects in another table.  I also had to ensure that the objects only seeded once.

```
private void SeedDonations()
{
  var donorSubscriber = (from x in context.Users
                        where x.Role == "Subscriber"
                        select x).FirstOrDefault();
                        
  var donorUser = (from x in context.Users
                  where x.Role == "User"
                  select x).FirstOrDefault();
                  
  var donations = new List<Donations>
  {
    new Donation {Donor = donorUser, DonationTime = new DateTime(2021, 1, 6), Amount = 100),
    new Donation {Donor = donorSubscriber, DonationTime = new DateTime(2021, 1, 6), Amount = 500),
    new Donation {Donor = donorSubscriber, DonationTime = new DateTime(2021, 1, 6), Amount = 250),
    new Donation {DonationTime = new DateTime(2021, 1, 6), Amount = 25)
  };
  
  donations.ForEach(donattion => context.donations.AddPrUpdate(d => new { d.Amount, d.DonationTime }, donation));
  context.SaveChanges();
  ```

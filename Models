// Models/ApplicationUser.cs
using Microsoft.AspNetCore.Identity;
using System.ComponentModel.DataAnnotations;

namespace LuxeApi.Models
{
    public class ApplicationUser : IdentityUser
    {
        [Required, MaxLength(50)]
        public string Name { get; set; } = string.Empty;

        public UserRole Role { get; set; } = UserRole.User;
        
        public string? Avatar { get; set; }
        
        public bool NewsletterSubscribed { get; set; } = true;
        
        public bool NotificationsEnabled { get; set; } = true;
        
        public string Currency { get; set; } = "USD";
        
        public DateTime? LastLogin { get; set; }
        
        public bool IsActive { get; set; } = true;
        
        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;
        
        public DateTime UpdatedAt { get; set; } = DateTime.UtcNow;

        // Navigation properties
        public virtual ICollection<UserAddress> Addresses { get; set; } = new List<UserAddress>();
    }

    public enum UserRole
    {
        User,
        Admin
    }
}

// ===========================================
// Models/Product.cs
using System.ComponentModel.DataAnnotations;

namespace LuxeApi.Models
{
    public class Product
    {
        public Guid Id { get; set; } = Guid.NewGuid();

        [Required, MaxLength(100)]
        public string Name { get; set; } = string.Empty;

        [Required, MaxLength(1000)]
        public string Description { get; set; } = string.Empty;

        [Required, Range(0, double.MaxValue)]
        public decimal Price { get; set; }

        [Range(0, double.MaxValue)]
        public decimal? ComparePrice { get; set; }

        [Required]
        public ProductCategory Category { get; set; }

        public string? Subcategory { get; set; }

        public string Brand { get; set; } = "LUXE";

        [Required]
        public string Sku { get; set; } = string.Empty;

        public List<string> Materials { get; set; } = new();

        public List<string> CareInstructions { get; set; } = new();

        public List<string> Tags { get; set; } = new();

        public bool IsActive { get; set; } = true;

        public bool IsFeatured { get; set; } = false;

        public string? SeoTitle { get; set; }

        public string? SeoDescription { get; set; }

        public double AverageRating { get; set; } = 0;

        public int RatingCount { get; set; } = 0;

        public int TotalStock { get; set; } = 0;

        public int SoldCount { get; set; } = 0;

        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

        public DateTime UpdatedAt { get; set; } = DateTime.UtcNow;

        // Navigation properties
        public virtual ICollection<ProductVariant> Variants { get; set; } = new List<ProductVariant>();
        public virtual ICollection<ProductImage> Images { get; set; } = new List<ProductImage>();
    }

    public enum ProductCategory
    {
        Basics,
        Formal,
        Outerwear,
        Dresses,
        Knitwear,
        Bottoms,
        Accessories
    }

    public class ProductVariant
    {
        public Guid Id { get; set; } = Guid.NewGuid();
        public Guid ProductId { get; set; }
        public ProductSize Size { get; set; }
        public string Color { get; set; } = string.Empty;
        public string ColorCode { get; set; } = string.Empty;
        public int Stock { get; set; } = 0;
        public string Sku { get; set; } = string.Empty;

        // Navigation properties
        public virtual Product Product { get; set; } = null!;
    }

    public class ProductImage
    {
        public Guid Id { get; set; } = Guid.NewGuid();
        public Guid ProductId { get; set; }
        public string Url { get; set; } = string.Empty;
        public string Alt { get; set; } = string.Empty;
        public bool IsPrimary { get; set; } = false;

        // Navigation properties
        public virtual Product Product { get; set; } = null!;
    }

    public enum ProductSize
    {
        XS, S, M, L, XL, XXL
    }
}

// ===========================================
// Models/Order.cs
using System.ComponentModel.DataAnnotations;

namespace LuxeApi.Models
{
    public class Order
    {
        public Guid Id { get; set; } = Guid.NewGuid();

        [Required]
        public string UserId { get; set; } = string.Empty;

        [Required]
        public string OrderNumber { get; set; } = string.Empty;

        [Required, Range(0, double.MaxValue)]
        public decimal Subtotal { get; set; }

        public decimal Tax { get; set; } = 0;

        public decimal ShippingCost { get; set; } = 0;

        public string ShippingMethod { get; set; } = "standard";

        public string? TrackingNumber { get; set; }

        public decimal DiscountAmount { get; set; } = 0;

        public string? DiscountCode { get; set; }

        [Required]
        public decimal Total { get; set; }

        public OrderStatus Status { get; set; } = OrderStatus.Pending;

        public PaymentStatus PaymentStatus { get; set; } = PaymentStatus.Pending;

        [Required]
        public PaymentMethod PaymentMethod { get; set; }

        public string? PaymentId { get; set; }

        public string? Notes { get; set; }

        public DateTime? EstimatedDelivery { get; set; }

        public DateTime? ActualDelivery { get; set; }

        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

        public DateTime UpdatedAt { get; set; } = DateTime.UtcNow;

        // Addresses (stored as JSON)
        public Address ShippingAddress { get; set; } = new();
        public Address? BillingAddress { get; set; }

        // Navigation properties
        public virtual ApplicationUser User { get; set; } = null!;
        public virtual ICollection<OrderItem> Items { get; set; } = new List<OrderItem>();
    }

    public class OrderItem
    {
        public Guid Id { get; set; } = Guid.NewGuid();
        public Guid OrderId { get; set; }
        public Guid ProductId { get; set; }
        public string Name { get; set; } = string.Empty;
        public decimal Price { get; set; }
        public int Quantity { get; set; }
        public decimal Subtotal { get; set; }

        // Variant info
        public ProductSize? Size { get; set; }
        public string? Color { get; set; }
        public string? Sku { get; set; }

        // Navigation properties
        public virtual Order Order { get; set; } = null!;
        public virtual Product Product { get; set; } = null!;
    }

    public class Address
    {
        public string Street { get; set; } = string.Empty;
        public string City { get; set; } = string.Empty;
        public string State { get; set; } = string.Empty;
        public string ZipCode { get; set; } = string.Empty;
        public string Country { get; set; } = string.Empty;
    }

    public enum OrderStatus
    {
        Pending,
        Confirmed,
        Processing,
        Shipped,
        Delivered,
        Cancelled,
        Refunded
    }

    public enum PaymentStatus
    {
        Pending,
        Paid,
        Failed,
        Refunded
    }

    public enum PaymentMethod
    {
        CreditCard,
        PayPal,
        ApplePay,
        GooglePay
    }
}

// ===========================================
// Models/Cart.cs
namespace LuxeApi.Models
{
    public class Cart
    {
        public Guid Id { get; set; } = Guid.NewGuid();
        public string UserId { get; set; } = string.Empty;
        public DateTime LastModified { get; set; } = DateTime.UtcNow;
        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

        // Navigation properties
        public virtual ApplicationUser User { get; set; } = null!;
        public virtual ICollection<CartItem> Items { get; set; } = new List<CartItem>();
    }

    public class CartItem
    {
        public Guid Id { get; set; } = Guid.NewGuid();
        public Guid CartId { get; set; }
        public Guid ProductId { get; set; }
        public int Quantity { get; set; }
        public DateTime AddedAt { get; set; } = DateTime.UtcNow;

        // Variant info
        public ProductSize? Size { get; set; }
        public string? Color { get; set; }
        public string? Sku { get; set; }

        // Navigation properties
        public virtual Cart Cart { get; set; } = null!;
        public virtual Product Product { get; set; } = null!;
    }
}

// ===========================================
// Models/UserAddress.cs
namespace LuxeApi.Models
{
    public class UserAddress
    {
        public Guid Id { get; set; } = Guid.NewGuid();
        public string UserId { get; set; } = string.Empty;
        public AddressType Type { get; set; }
        public string Street { get; set; } = string.Empty;
        public string City { get; set; } = string.Empty;
        public string State { get; set; } = string.Empty;
        public string ZipCode { get; set; } = string.Empty;
        public string Country { get; set; } = string.Empty;
        public bool IsDefault { get; set; } = false;
        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

        // Navigation properties
        public virtual ApplicationUser User { get; set; } = null!;
    }

    public enum AddressType
    {
        Shipping,
        Billing
    }
}

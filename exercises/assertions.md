# On assertions

Answer the following questions:

1. The following assertion fails `assertTrue(3 * .4 == 1.2)`. Explain why and describe how this type of check should be done.

Answer 1)- It fails because of the java assertion error because the statement is believed to be true but is actually false and creates an exception.
         - In order to avoid the java assertion exception we need to do exceptional handling by using the try catch block.

2. What is the difference between `assertEquals` and `assertSame`? Show scenarios where they produce the same result and scenarios where they do not produce the same result.
Answer 2)- assertEquals checks whether the two values are equal or not and assertSame checks whether the two objects belongs to the same object or not. It compares the reference            between two objects.
           Scenario when both gives the same result because the method is not overridden.
            public class AES {

                  private int i;
                  public AES(int i){ this.i = i; }


            }
            public class test2 {

              final AES a1 = new AES(0);
                final AES a2 = new AES(0);

                @Test
                public void assertsame_testAssertSame(){
                    assertSame(a1, a2); 
                }

                @Test
                public void assertsame_testAssertEquals(){
                    assertEquals(a1, a2); 
                }
            }
            Scenario where both gives different result.
            public class AES {

                  private int i;
                  public AES(int i){ this.i = i; }

                  @Override
                  public boolean equals(Object o){
                      // self check
                      if(this == o){ return true; } else
                      // null check
                      if(o == null){ return false;} else
                      // type check and cast
                      if(getClass() != o.getClass()){ return false; } else {
                          final AES a = (AES) o;
                          // field comparison
                          return Objects.equals(a, a);
                      }
                  }
            }

3. In classes we saw that `fail` is useful to mark code that should not be executed because an exception was expected before. Find other uses for `fail`. Explain the use case and add an example.
Answer 3)-Uses of fail
        • mark a test that is incomplete, so it fails and warns you until you can finish it
        • making sure an exception is thrown
               Example of exception thrown
                try{

              fail("Exception not thrown");
            }catch(Exception e){
              assertTrue(e.hasSomeFlag());
            }

4. In JUnit 4, an exception was expected using the `@Test` annotation, while in JUnit 5 there is a special assertion method `assertThrows`. In your opinion, what are the advantages of this new way of checking expected exceptions?
Answer 4)- assertThrows assertion allows us a clear and a simple way to assert if an executable throws the specified exception type.
            @Test
            void AssertingException() {
                Throwable exception = assertThrows(
                  IllegalArgumentException.class, 
                  () -> {
                      throw new IllegalArgumentException("Exception message");
                  }
                );
                assertEquals("Exception message", exception.getMessage());
            }
